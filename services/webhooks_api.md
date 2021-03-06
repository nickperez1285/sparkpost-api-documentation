# Webhooks [/webhooks]

# Group Webhooks

The Webhooks API provides the means to create, review, update, and delete webhooks, which enables you to
receive push updates of the raw events generated by SparkPost.

## Writing a Consumer

To successfully write a consumer application of the Webhooks API, you must understand the events being pushed, as well as their data structure.  Events are categorized as message, generation, engagement, or unsubscribe.



### Message Events

Message events describe the life cycle of a message including injection, delivery, and disposition.

#### Event Types

+ **Injection** - Message is received by or injected into SparkPost.

+ **Delivery** - Remote MTA acknowledged receipt of a message.

+ **Delay** - Remote MTA has temporarily rejected a message.

+ **Out-of-Band** - Remote MTA initially reported acceptance of a message, but it has since asynchronously reported that the message was not delivered.

+ **Bounce** - Remote MTA has permanently rejected a message.

+ **Policy Rejection** - Due to policy, SparkPost rejected a message or failed to generate a message.

+ **Spam Complaint** - Message was classified as spam, whether manually or programmatically.

#### Envelope
Each message event is supplied in the following JSON envelope:

  ```
  {
    msys: {
      message_event: {}
    }
  }
  ```

* * *

### Generation Events

Generation events provide insight into message generation failures or rejections.

#### Event Types

+ **Generation Failure** - Message generation failed for an intended recipient.

+ **Generation Rejection** - SparkPost rejected message generation due to policy.

#### Envelope
Each generation event is supplied in the following JSON envelope:
  ```
  {
    msys: {
      gen_event: {}
    }
  }
  ```

* * *

### Engagement Events

Engagement events describe the behavior of a recipient with respect to the message sent.

#### Event Types

+ **Open** - Recipient opened a message in a mail client, thus rendering a tracking pixel.

+ **Click** - Recipient clicked a tracked link in a message, thus prompting a redirect through the
SparkPost click-tracking server to the link's destination.

#### Envelope
Each engagement event is supplied in the following JSON envelope:
  ```
  {
    msys: {
      track_event: {}
    }
  }
  ```
* * *

### Unsubscribe Events

Unsubscribe events provide insight into the action the user performed to become unsubscribed.

#### Event Types

+ **List Unsubscribe** - User clicked the "unsubscribe" button on an email client.

+ **Link Unsubscribe** - User clicked a hyperlink in a received email.

#### Envelope
Each unsubscribe event is supplied in the following JSON envelope:
  ```
  {
    msys: {
      unsubscribe_event: {}
    }
  }
  ```
### Field Definitions

A batch of event data transmitted to a webhook consists of one or more event records, each composed
of a payload wrapped in a type-specific envelope as described for each event type.

The following fields may appear in an event record payload.  Not all event types use all of these
fields.  See the Event-to-Field Mapping section for details about which fields appear in a given event type's payload.

| Key                   | Type          | Description                                                                                    |
| --------------------- | ------------- | --------------------------------                                                               |
| accept_language  | string | Value of the browser's Accept header (e.g. en-US,en;q=0.5) |
| bounce_class     | string | Classification code for a given message (see [Bounce Classification Codes](https://www.sparkpost.com/docs/bounce-classification-codes)) |
| campaign_id           | string        | Campaign of which this message was a part                                                      |
| customer_id           | string        | SparkPost-customer identifier through which this message was sent                               |
| error_code       | string | Error code by which the remote server described a failed delivery attempt                                                                                                                       |
| fbtype           | string | Type of spam report entered against this message (see [RFC 5965 § 7.3](http://tools.ietf.org/html/rfc5965#section-7.3))                                                                         |
| friendly_from       | string    | Friendly sender or "From" header in the original email |
| ip_address       | string | IP address of the host to which SparkPost delivered this message; in engagement events, the IP address of the host where the HTTP request originated |
| geo_ip           | object | Geographic location based on the IP address, including latitude, longitude, city, country, and region                                                 |
| mailfrom            | string        | Envelope mailfrom of the original email                                       |
| message_id            | string        | SparkPost-cluster-wide unique identifier for this message                                       |
| msg_from         | string | Sender address used on this message's SMTP envelope                                                                                                                                             |
| msg_size         | string | Message's size in bytes                                                                                                                                                                         |
| num_retries      | string | Number of failed attempts before this message was successfully delivered; when the first attempt succeeds, zero                                                                                 |
| queue_time       | string | Delay, expressed in milliseconds, between this message's injection into SparkPost and its delivery to the receiving domain; that is, the length of time this message spent in the outgoing queue |
| rcpt_meta             | object        | Metadata describing the message recipient                                                      |
| rcpt_subs        | object | Substitutions applied to the template to construct this message                                                                                                                                 |
| rcpt_tags             | array         | Tags applied to the message which generated this event                                         |
| rcpt_to          | string | Recipient address used on this message's SMTP envelope                                                                                                                                           |
| reason           | string | Raw text of the response by which the remote server described a failed delivery attempt                                                                                                         |
| remote_addr      | string | IP address of the host from which SparkPost received this message                                                                                                                                |
| report_by        | string | Address of the entity reporting this message as spam                                                                                                                                            |
| report_to        | string | Address to which this spam report is to be delivered                                                                                                                                            |
| routing_domain   | string | Domain receiving this message                                                                                                                                                                   |
| target_link_name | string | Name of the link for which a click event was generated                                                                                                                                          |
| target_link_url  | string | URL of the link for which a click event was generated                                                                                                                                           |
| template_id      | string | Slug of the template used to construct this message                                                                                                                                             |
| template_version | string | Version of the template used to construct this message                                                                                                                                          |
| timestamp             | timestamp     | Event date and time, in Unix timestamp format (integer seconds since 00:00:00 GMT 1970-01-01) |
| transactional       | string    | Indicates if this event occurred on a transactional email |
| transmission_id       | string        | Transmission which originated this message                                                     |
| type                  | string        | Type of event this record describes                                                            |
| user_agent       | string | Value of the browser's User-Agent header (e.g. Mozilla/5.0 (Macintosh; U; PPC Mac OS X; en) AppleWebKit/125.2 (KHTML, like Gecko) Safari/125.8)                                                                            |
## Event-to-Field Mapping

Not all fields are meaningful for all event types.  The following is a mapping of event type to fields that constitute its payload.

Not every event of a given type will include every field listed here. Only those fields with meaningful values for a specific event will be included.

| Category              | Event Type             | Field Types                                                                                                                                                     |
| --------------------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Message Events    | Injection            | campaign_id, customer_id, friendly_from, message_id, msg_from, msg_size, rcpt_to, routing_domain, template_id, timestamp, transactional, type|
|                   | Delivery             | campaign_id, customer_id, friendly_from, ip_address, message_id, msg_from, msg_size, num_retries, queue_time, rcpt_meta, rcpt_tags, rcpt_to, routing_domain, template_id, template_version, timestamp, transmission_id, transactional, type |
|                   | Delay                | bounce_class, campaign_id, customer_id, error_code, friendly_from, ip_address, message_id, msg_from, msg_size, num_retries, queue_time, rcpt_meta, rcpt_tags, rcpt_to, reason, routing_domain, template_id, template_version, timestamp, transactional, transmission_id, type|
|                   | Out-of-Band          | bounce_class, campaign_id, customer_id, error_code, friendly_from, message_id, msg_from, rcpt_to, reason, routing_domain, template_id, timestamp, transactional, type|
|                   | Bounce               | bounce_class, campaign_id, customer_id, error_code, friendly_from, ip_address, message_id, msg_from, msg_size, num_retries, rcpt_meta, rcpt_tags, rcpt_to, reason, routing_domain, template_id, template_version, timestamp, transactional, transmission_id, type|
|                   | Policy Rejection     | campaign_id, customer_id, error_code, friendly_from, message_id, msg_from, rcpt_meta, rcpt_tags, rcpt_to, reason, remote_addr, routing_domain, template_id, template_version, timestamp, transactional, transmission_id, type|
|                   | Spam Complaint       | campaign_id, customer_id, fbtype, friendly_from, rcpt_to, report_by, report_to, template_id, timestamp, transactional, type, user_str |
| Generation Events | Generation Failure   | campaign_id, customer_id, friendly_from, message_id, rcpt_meta, rcpt_subs, rcpt_tags, rcpt_to, reason, routing_domain, template_id, template_version, timestamp, transactional, transmission_id, type|
|                   | Generation Rejection | campaign_id, customer_id, error_code, friendly_from, message_id, rcpt_meta, rcpt_subs, rcpt_tags, rcpt_to, reason, routing_domain, template_id, template_version, timestamp, transactional, transmission_id, type|
| Engagement Events | Open                 | accept_language, campaign_id, customer_id, friendly_from, geo_ip, ip_address, message_id, rcpt_meta, rcpt_tags, rcpt_to, template_id, template_version, timestamp, transactional, transmission_id, type, user_agent|
|                   | Click                | accept_language, campaign_id, customer_id, friendly_from, geo_ip, ip_address, message_id, rcpt_meta, rcpt_tags, rcpt_to, target_link_name, target_link_url, template_id, template_version, timestamp, transactional, transmission_id, type, user_agent|
| Unsubscribe Events | List Unsubscribe    | campaign_id, customer_id, friendly_from, mailfrom, message_id, rcpt_meta, rcpt_tags, rcpt_to, template_id, template_version, timestamp, transactional, transmission_id, type|
|                   | Link Unsubscribe     | campaign_id, customer_id, friendly_from, mailfrom, message_id, rcpt_meta, rcpt_tags, rcpt_to, template_id, template_version, timestamp, transactional, transmission_id, type, user_agent|


## Webhook Object Properties

| Property   | Type   | Description | Required | Notes |
|------------|--------|-------------|----------|-------|
| name       | string | User-friendly name for webhook | yes | example: `Example webhook` |
| target     | string | URL of the target to which to POST event batches | yes |  When a webhook is created or updated with a change to this property, a test POST request is sent to the given URL. The target URL must accept the connection and respond with HTTP 200; otherwise, your request to the Webhook API will fail with HTTP 400, and the requested change will not be applied.<br />example: `http://client.example.com/example-webhook` |
| auth_token | string | Authentication token to present in the X-MessageSystems-Webhook-Token header of POST requests to target | no | Use this token in your target application to confirm that data is coming from the Webhooks API. <br />example: `5ebe2294ecd0e0f08eab7690d2a6ee69`|
| events     | array  | Array of event types this webhook will receive | yes | Acceptable values include: `delivery`, `injection`, `policy_rejection`, `spam_complaint`, `delay`, `bounce`, `out_of_band`, `open`, `click`, `generation_failure`, `generation_rejection`, `list_unsubscribe`, `link_unsubscribe` <br />example: `["delivery", "injection", "open", "click"]`|

## Webhooks Collection [/webhooks{?timezone}]

+ Model

    + Body

        ```
        {
          "results": [
            {
              "id": "12affc24-f183-11e3-9234-3c15c2c818c2",
              "name": "Example webhook",
              "target": "http://client.example.com/example-webhook",
              "auth_token": "5ebe2294ecd0e0f08eab7690d2a6ee69",
              "events": [
                "delivery",
                "injection",
                "open",
                "click"
              ],
              "last_successful": "2014-07-01 16:09:15",
              "last_failure": "2014-08-01 15:15:45",
              "links": [
                {
                  "href": "http://www.messagesystems-api-url.com/api/v1/webhooks/a2b83490-10df-11e4-b670-c1ffa86371ff",
                  "rel": "urn.msys.webhooks.webhook",
                  "method": ["GET","PUT"]
                }
              ]
            },
            {
              "id": "123456-abcd-efgh-7890-123445566778",
              "name": "Better webhook",
              "target": "http://client.example.com/another-example",
              "auth_token": "",
              "events": [
                "generation_rejection",
                "generation_failure"
              ],
              "links": [
                {
                  "href": "http://www.messagesystems-api-url.com/api/v1/webhooks/123456-abcd-efgh-7890-123445566778",
                  "rel": "urn.msys.webhooks.webhook",
                  "method": ["GET","PUT"]
                }
              ]
            }
          ]
        }
        ```

### List all Webhooks [GET]

List currently extant webhooks.

+ Parameters
  + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

    [Webhooks Collection][]

### Create a Webhook [POST]

Create a webhook by providing a **webhook object** as the POST request body.  On creation, events will
begin to be pushed to the target URL specified in the POST request body.

As described in "Webhook Object Properties", webhook creation entails a test POST request to the URL given as the _target_ value. If this request does not receive an HTTP 200 response, your request to the Webhook API will fail with HTTP 400, and the webhook will not be created.

+ Request (application/json)

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf

    + Body

        ```
        {
          "name": "Example webhook",
          "target": "http://client.example.com/example-webhook",
          "auth_token": "5ebe2294ecd0e0f08eab7690d2a6ee69",
          "events": [
            "delivery",
            "injection",
            "open",
            "click"
          ]
        }
        ```

+ Response 200 (application/json)

    ```
    {
      "results": {
        "id": "12affc24-f183-11e3-9234-3c15c2c818c2",
        "links": [
          {
            "href": "http://www.messagesystems-api-url.com/api/v1/webhooks/12affc24-f183-11e3-9234-3c15c2c818c2",
            "rel": "urn.msys.webhooks.webhook",
            "method": ["GET","PUT"]
          }
        ]
      }
    }
    ```

## Webhooks Resource [/webhooks/{id}{?timezone}]

+ Model

    + Body

        ```
        {
        "results": {
          "name": "Example webhook",
          "target": "http://client.example.com/example-webhook",
          "auth_token": "5ebe2294ecd0e0f08eab7690d2a6ee69",
          "events": [
            "delivery",
            "injection",
            "open",
            "click"
          ],
          "links": [
            {
              "href": "http://www.messagesystems-api-url.com/api/v1/webhooks/12affc24-f183-11e3-9234-3c15c2c818c2/validate",
              "rel": "urn.msys.webhooks.validate",
              "method": ["POST"]
            },
            {
              "href": "http://www.messagesystems-api-url.com/api/v1/webhooks/12affc24-f183-11e3-9234-3c15c2c818c2/batch-status",
              "rel": "urn.msys.webhooks.batches",
              "method": ["GET"]
            }
          ]
        }
        }
        ```

### Describe a Webhook [GET]

Retrieve details about a webhook by specifying its id in the URI path.

+ Parameters
  + id (required, uuid, `12affc24-f183-11e3-9234-3c15c2c818c2`) ... UUID identifying a webhook
  + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

    [Webhooks Resource][]

## Update/Delete a Webhook [/webhooks/{id}]

### Update a Webhook [PUT]

Modify a webhook's properties by specifying its id in the URI path and use a **webhook object** as
the PUT request body.

Note that batches currently queued for delivery to this webhook will not be affected by these
modifications.  For example, if you change the webhook's target URL, batches already queued for delivery will still be POSTed to the previous URL.

As described in "Webhook Object Properties", a change to the _target_ value entails a test POST request to the URL given. If this request does not receive an HTTP 200 response, your request to the Webhook API will fail with HTTP 400, and the webhook will not be modified.

+ Parameters
  + id (required, uuid, `12affc24-f183-11e3-9234-3c15c2c818c2`) ... UUID identifying a webhook

+ Request (application/json)

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf

    + Body

        ```
        {
          "name": "Renamed webhook",
          "events": [
            "rejection",
            "delay"
          ]
        }
        ```

+ Response 200 (application/json)

    ```
    {
      "results": {
        "id": "12affc24-f183-11e3-9234-3c15c2c818c2",
        "links": [
          {
            "href": "http://www.messagesystems-api-url.com/api/v1/webhooks/12affc24-f183-11e3-9234-3c15c2c818c2/validate",
            "rel": "urn.msys.webhooks.validate",
            "method": ["POST"]
          }
        ]
      }
    }
    ```

### Delete a Webhook [DELETE]

Delete a webhook from the system by specifying its id in the URI path.  The system will stop pushing data to the target URL after the batches currently queued to be
delivered are drained.

+ Parameters
  + id (required, uuid, `12affc24-f183-11e3-9234-3c15c2c818c2`) ... UUID identifying a webhook

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf

+ Response 204

## Webhooks Validation [/webhooks/{id}/validate]

### Validate a Webhook [POST]

The validation sends an example message event batch from the Webhook API to the
target URL, validates that the target responds with HTTP 200,
and returns detailed information on the response received from the target.

#### Message Properties

| Property   | Type   | Description | Required | Notes |
|------------|--------|-------------|----------|-------|
| message    | object | Example batch to send | yes | See "Writing a Consumer" for a more detailed example.<br />example: `{"msys": {}}`  |

+ Parameters
  + id (required, uuid, `12affc24-f183-11e3-9234-3c15c2c818c2`) ... UUID identifying a webhook

+ Request (application/json)

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf

    + Body

        ```
        {
            "message": {
                "msys": {}
            }
        }
        ```

+ Response 200 (application/json)

    ```
    {
      "results": {
        "msg": "Test POST to endpoint succeeded",
        "response": {
          "status": 200,
          "headers": {
            "content-type": "text/plain"
          },
          "body": "OK"
        }
      }
    }
    ```

## Webhooks Batch Status [/webhooks/{id}/batch-status{?timezone}]

### Retrieve Status Information [GET]

Retrieve status information regarding batches that have been generated
for the given webhook by specifying its id in the URI path. Status information includes the successes of batches
that previously failed to reach the webhook's target URL and batches that
are currently in a failed state.

+ Parameters
  + id (required, uuid, `12affc24-f183-11e3-9234-3c15c2c818c2`) ... UUID identifying a webhook
  + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

    ```
    {
      "results": [
        {
          "batch_id": "032d330540298f54f0e8bcc1373f3cfd",
          "ts": "2014-07-30T21:38:08.000Z",
          "attempts": 7,
          "response_code": 200
        },
        {
          "batch_id": "13c6764994a8f6b4e29906d5712ca7d",
          "ts": "2014-07-30T20:38:08.000Z",
          "attempts": 2,
          "response_code": 400
        }
      ]
    }
    ```
