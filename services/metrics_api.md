# Metrics [/metrics]

# Group Metrics

SparkPost logs copious amounts of statistical, real-time data about message processing, message
disposition, and campaign performance.  This reporting data is available in the UI or through the Metrics API.  The Metrics API provides a variety of endpoints enabling you to retrieve a summary of the data, data grouped by a specific qualifier, or data by event type.  Within each endpoint, you can also apply various filters to drill down to the data for your specific reporting needs.

## Metrics API Deliverability Glossary

Definitions for terms found in Metrics API

| Term     | Definition    |
|---------:|:--------------|
|`count_targeted` | Messages successfully injected into SparkPost as well as rejected by it|
|`count_injected` | Messages injected to or received by SparkPost|
|`count_sent` | Messages that SparkPost attempted to deliver, which includes both Deliveries and In-Band Bounces|
|`count_accepted` | Messages an ISP or other remote domain accepted (less Out-of-Band Bounces)|
|`count_delivered_first` | Messages delivered on the first attempt|
|`count_delivered_subsequent` | Messages delivered that required more than one delivery attempt|
|`count_rendered` | Total renderings of a message|
|`count_unique_rendered` | Total number of messages that were rendered at least once|
|`count_unique_confirmed_opened` | Total number of messages that were rendered or had at least one link selected|
|`count_clicked` | Total number of times that links were selected across all messages|
|`count_unique_clicked` | Total number of messages which had at least one link selected one or more times|
|`count_bounce` | Total number of bounced messages, which includes both In-Band and Out-of-Band bounces|
|`count_hard_bounce` | Total number of Bounced messages due to hard bounce classification reasons|
|`count_soft_bounce` | Total number of Bounced messages due to soft bounce classification reasons|
|`count_block_bounce` | Total number of Bounced messages due to an IP block|
|`count_admin_bounce` | Total number of Bounced messages due to admin bounce classification reasons, also includes Rejected|
|`count_undetermined_bounce` | Total number of Bounced messages due to undetermined bounce reasons|
|`count_rejected` | Messages rejected due to policy or that failed to generate|
|`count_policy_rejection` | Messages rejected by SparkPost due to policy|
|`count_generation_failed` | Message generation failed for an intended recipient|
|`count_generation_rejection` | Messages rejected by SparkPost due to policy|
|`open_rate` | Percentage of Targeted messages that were rendered or had at least one link selected|
|`click_through_rate` | Percentage of Targeted messages that had at least one link selected|
|`bounce_rate` | Percentage of Targeted messages that Bounced|
|`hard_bounce_rate` | Percentage of Targeted messages that Hard Bounced|
|`soft_bounce_rate` | Percentage of Targeted messages that Soft Bounced|
|`block_bounce_rate` | Percentage of Targeted messages that Block Bounced|
|`admin_bounce_rate` | Percentage of Targeted messages that Admin Bounced|
|`undetermined_bounce_rate` | Percentage of Targeted messages that Undetermined Bounced|
|`count_inband_bounce` | Messages that bounced on delivery attempt during the SMTP session|
|`count_outofband_bounce` | Messages that the ISP bounced subsequent to a successful delivery|
|`count_delayed` | Total number of delays due to any temporary failure|
|`count_delayed_first` | Messages delayed on the first delivery attempt|
|`avg_delivery_time_first` | Average delivery time in milliseconds (latency) for messages delivered on the first attempt|
|`avg_delivery_time_subsequent` | Average delivery time in milliseconds (latency) for messages delivered that required more than one attempt|
|`avg_msg_size` | Average size of delivered messages, in bytes (including attachments)|
|`total_msg_volume` | Total size of delivered messages, in bytes (including attachments)|
|`count_spam_complaint` | Number of spam complaints received from an ISP|

## Metrics Discoverability Links [/metrics/]

The Metrics API is designed for discoverability of child links.  Calling the API root displays a
list of URIs that exists within the Metrics API.

+ Model (application/json)

    + Body

        ```
        {
            "results": {},
            "links": [
                {
                   "href": "/api/v1/metrics/",
                   "rel": "",
                   "method": "GET"
                },
                {
                  "href": "/api/v1/metrics/campaigns",
                  "rel": "campaigns",
                  "method": "GET"
                },
                {
                  "href": "/api/v1/metrics/deliverability",
                  "rel": "deliverability",
                  "method": "GET"
                },
                {
                  "href": "/api/v1/metrics/domains",
                  "rel": "domains",
                  "method": "GET"
                }
            ]
        }
        ```

    + Schema

        ```
        {
            "type":"object",
            "$schema": "http://json-schema.org/draft-03/schema",
            "required":false,
            "properties":{
                "links": {
                    "type":"array",
                    "required":false,
                    "items":
                        {
                            "type":"object",
                            "required":false,
                            "properties":{
                                "href": {
                                    "type":"string",
                                    "required":false
                                },
                                "method": {
                                    "type":"string",
                                    "required":false
                                },
                                "rel": {
                                    "type":"string",
                                    "required":false
                                }
                            }
                        }
                },
                "results": {
                    "type":"object",
                    "required":false
                }
            }
        }
        ```

### Metrics Discoverability Links [GET]

Provides links to all child URIs within the Metrics API.

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200

    [Metrics Discoverability Links][]


## Deliverability Metrics [/metrics/deliverability{?from,to,domains,campaigns,templates,sandbox,metrics,timezone}]


+ Model

    + Body

        ```
        {
          "results": [
            {
              "count_targeted": 34432,
              "count_injected": 32323,
              "count_rejected": 2343,
              "count_sent": 34344
            }
          ],
        "links": [
            {
                "href": "/api/v1/metrics/deliverability",
                "rel": "deliverability",
                "method": "GET"
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "links": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "href": {
                      "type":"string",
                      "required":false
                    },
                    "method": {
                      "type":"string",
                      "required":false
                    },
                    "rel": {
                      "type":"string",
                      "required":false
                    }
                  }
                }
            },
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "count_accepted": {
                      "type":"number",
                      "required":false
                    },
                    "count_admin_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_block_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_failed": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_hard_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_inband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_injected": {
                      "type":"number",
                      "required":false
                    },
                    "count_outofband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_policy_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_rejected": {
                      "type":"number",
                      "required":false
                    },
                    "count_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "count_sent": {
                      "type":"number",
                      "required":false
                    },
                    "count_soft_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_spam_complaint": {
                      "type":"number",
                      "required":false
                    },
                    "count_targeted": {
                      "type":"number",
                      "required":false
                    },
                    "count_undetermined_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_confirmed_opened": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "total_delivery_time_first": {
                      "type":"number",
                      "required":false
                    },
                    "total_delivery_time_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "total_msg_volume": {
                      "type":"number",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Deliverability Metrics Summary [GET]

Provides high-level summary of aggregate metrics and lists the child endpoints that contain
aggregate data, which can be used as "group by" qualifiers.

+ Parameters
    + from (required, datetime, `2014-07-11T08:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + to = `now` (optional, datetime, `2014-07-20T09:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + domains (optional, list, `gmail.com,yahoo.com,hotmail.com`) ... Comma-delimited list of domains to include
    + campaigns (optional, list, `Black Friday`) ... Comma-delimited list of campaigns to include
    + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
    + sandbox (optional, string, `true`) ... Restrict the query to events generated with a sandbox sending domain
    + metrics (required, list) ... Comma-delimited list of metrics for filtering

        + Values
            + `count_injected`
            + `count_bounce`
            + `count_rejected`
            + `count_delivered`
            + `count_delivered_first`
            + `count_delivered_subsequent`
            + `total_delivery_time_first`
            + `total_delivery_time_subsequent`
            + `total_msg_volume`
            + `count_policy_rejection`
            + `count_generation_rejection`
            + `count_generation_failed`
            + `count_inband_bounce`
            + `count_outofband_bounce`
            + `count_soft_bounce`
            + `count_hard_bounce`
            + `count_block_bounce`
            + `count_admin_bounce`
            + `count_undetermined_bounce`
            + `count_delayed`
            + `count_delayed_first`
            + `count_rendered`
            + `count_unique_rendered`
            + `count_unique_confirmed_opened`
            + `count_clicked`
            + `count_unique_clicked`
            + `count_targeted`
            + `count_sent`
            + `count_accepted`
            + `count_spam_complaint`

    + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

  [Deliverability Metrics][]



## Deliverability Metrics by Domain [/metrics/deliverability/domain{?from,to,domains,campaigns,templates,sandbox,metrics,timezone,order_by,limit}]

+ Model

    + Body

        ```
        {
          "results": [
            {
              "domain": "aol.com",
              "count_targeted": 34432,
              "count_injected": 32323,
              "count_rejected": 2343,
              "count_sent": 34344
            },
            {
              "domain": "foo.net",
              "count_targeted": 34432,
              "count_injected": 32323,
              "count_rejected": 2343,
              "count_sent": 34344
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "count_accepted": {
                      "type":"number",
                      "required":false
                    },
                    "count_admin_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_block_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_failed": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_hard_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_inband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_injected": {
                      "type":"number",
                      "required":false
                    },
                    "count_outofband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_policy_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_rejected": {
                      "type":"number",
                      "required":false
                    },
                    "count_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "count_sent": {
                      "type":"number",
                      "required":false
                    },
                    "count_soft_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_spam_complaint": {
                      "type":"number",
                      "required":false
                    },
                    "count_targeted": {
                      "type":"number",
                      "required":false
                    },
                    "count_undetermined_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_confirmed_opened": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "domain": {
                      "type":"string",
                      "required":false
                    },
                    "total_delivery_time_first": {
                      "type":"number",
                      "required":false
                    },
                    "total_delivery_time_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "total_msg_volume": {
                      "type":"number",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Deliverability Metrics by Domain [GET]

Provides aggregate metrics grouped by domain over the time window specified.

+ Parameters
  + from (required, datetime, `2014-07-11T08:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
  + to = `now` (optional, datetime, `2014-07-20T09:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
  + domains (optional, list, `gmail.com,yahoo.com,hotmail.com`) ... Comma-delimited list of domains to include
  + campaigns (optional, list, `Black Friday`) ... Comma-delimited list of campaigns to include
  
  + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
  + sandbox (optional, string, `true`) ... Restrict the query to events generated with a sandbox sending domain
  
  + metrics (required, list) ... Comma-delimited list of metrics for filtering
        
        + Values
            + `count_injected`
            + `count_bounce`
            + `count_rejected`
            + `count_delivered`
            + `count_delivered_first`
            + `count_delivered_subsequent`
            + `total_delivery_time_first`
            + `total_delivery_time_subsequent`
            + `total_msg_volume`
            + `count_policy_rejection`
            + `count_generation_rejection`
            + `count_generation_failed`
            + `count_inband_bounce`
            + `count_outofband_bounce`
            + `count_soft_bounce`
            + `count_hard_bounce`
            + `count_block_bounce`
            + `count_admin_bounce`
            + `count_undetermined_bounce`
            + `count_delayed`
            + `count_delayed_first`
            + `count_rendered`
            + `count_unique_rendered`
            + `count_unique_confirmed_opened`
            + `count_clicked`
            + `count_unique_clicked`
            + `count_targeted`
            + `count_sent`
            + `count_accepted`
            + `count_spam_complaint`
            
  + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`
  + limit (optional, int, `5`) ... Maximum number of results to return
  + order_by (optional, string, `count_injected`) ... Metric by which to order results

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

  [Deliverability Metrics by Domain][]




## Deliverability Metrics by Campaign [/metrics/deliverability/campaign{?from,to,domains,campaigns,templates,sandbox,metrics,timezone,limit,order_by}]


+ Model

    + Body

        ```
        {
          "results": [
            {
              "campaign_id": "campaign-0",
              "count_targeted": 34432,
              "count_injected": 32323,
              "count_rejected": 2343,
              "count_sent": 34344
            },
            {
              "campaign_id": "campaign-1",
              "count_targeted": 34432,
              "count_injected": 32323,
              "count_rejected": 2343,
              "count_sent": 34344
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "campaign_id": {
                      "type":"string",
                      "required":false
                    },
                    "count_accepted": {
                      "type":"number",
                      "required":false
                    },
                    "count_admin_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_block_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_failed": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_hard_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_inband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_injected": {
                      "type":"number",
                      "required":false
                    },
                    "count_outofband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_policy_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_rejected": {
                      "type":"number",
                      "required":false
                    },
                    "count_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "count_sent": {
                      "type":"number",
                      "required":false
                    },
                    "count_soft_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_spam_complaint": {
                      "type":"number",
                      "required":false
                    },
                    "count_targeted": {
                      "type":"number",
                      "required":false
                    },
                    "count_undetermined_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_confirmed_opened": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "total_delivery_time_first": {
                      "type":"number",
                      "required":false
                    },
                    "total_delivery_time_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "total_msg_volume": {
                      "type":"number",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Deliverability Metrics by Campaign [GET]

Provides aggregate metrics grouped by campaign over the time window specified.

+ Parameters
    + from (required, datetime, `2014-07-11T08:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + to = `now` (optional, datetime, `2014-07-20T09:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + domains (optional, list, `gmail.com,yahoo.com,hotmail.com`) ... Comma-delimited list of domains to include
    + campaigns (optional, list, `Black Friday`) ... Comma-delimited list of campaigns to include
    + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
    + sandbox (optional, string, `true`) ... Restrict the query to events generated with a sandbox sending domain
    + metrics (required, list) ... Comma-delimited list of metrics for filtering
      
        + Values
            + `count_injected`
            + `count_bounce`
            + `count_rejected`
            + `count_delivered`
            + `count_delivered_first`
            + `count_delivered_subsequent`
            + `total_delivery_time_first`
            + `total_delivery_time_subsequent`
            + `total_msg_volume`
            + `count_policy_rejection`
            + `count_generation_rejection`
            + `count_generation_failed`
            + `count_inband_bounce`
            + `count_outofband_bounce`
            + `count_soft_bounce`
            + `count_hard_bounce`
            + `count_block_bounce`
            + `count_admin_bounce`
            + `count_undetermined_bounce`
            + `count_delayed`
            + `count_delayed_first`
            + `count_rendered`
            + `count_unique_rendered`
            + `count_unique_confirmed_opened`
            + `count_clicked`
            + `count_unique_clicked`
            + `count_targeted`
            + `count_sent`
            + `count_accepted`
            + `count_spam_complaint`
            
    + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`
    + limit (optional, int, `5`) ... Maximum number of results to return
    + order_by (optional, string, `count_injected`) ... Metric by which to order results

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

  [Deliverability Metrics by Campaign][]


## Deliverability Metrics by Template [/metrics/deliverability/template{?from,to,domains,campaigns,templates,sandbox,metrics,timezone,limit,order_by}]


+ Model

    + Body

        ```
        {
          "results": [
            {
              "template_id": "template-0",
              "count_targeted": 34432,
              "count_injected": 32323,
              "count_rejected": 2343,
              "count_sent": 34344
            },
            {
              "template_id": "template-1",
              "count_targeted": 34432,
              "count_injected": 32323,
              "count_rejected": 2343,
              "count_sent": 34344
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "count_accepted": {
                      "type":"number",
                      "required":false
                    },
                    "count_admin_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_block_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_failed": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_hard_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_inband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_injected": {
                      "type":"number",
                      "required":false
                    },
                    "count_outofband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_policy_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_rejected": {
                      "type":"number",
                      "required":false
                    },
                    "count_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "count_sent": {
                      "type":"number",
                      "required":false
                    },
                    "count_soft_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_spam_complaint": {
                      "type":"number",
                      "required":false
                    },
                    "count_targeted": {
                      "type":"number",
                      "required":false
                    },
                    "count_undetermined_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_confirmed_opened": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "template_id": {
                      "type":"string",
                      "required":false
                    },
                    "total_delivery_time_first": {
                      "type":"number",
                      "required":false
                    },
                    "total_delivery_time_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "total_msg_volume": {
                      "type":"number",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Deliverability Metrics by Template [GET]

Provides aggregate metrics grouped by template over the time window specified.

+ Parameters
    + from (required, datetime, `2014-07-11T08:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + to = `now` (optional, datetime, `2014-07-20T09:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + domains (optional, list, `gmail.com,yahoo.com,hotmail.com`) ... Comma-delimited list of domains to include
    + campaigns (optional, list, `Black Friday`) ... Comma-delimited list of campaigns to include
    + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
    + sandbox (optional, string, `true`) ... Restrict the query to events generated with a sandbox sending domain
    + metrics (required, list) ... Comma-delimited list of metrics for filtering
      
        + Values
            + `count_injected`
            + `count_bounce`
            + `count_rejected`
            + `count_delivered`
            + `count_delivered_first`
            + `count_delivered_subsequent`
            + `total_delivery_time_first`
            + `total_delivery_time_subsequent`
            + `total_msg_volume`
            + `count_policy_rejection`
            + `count_generation_rejection`
            + `count_generation_failed`
            + `count_inband_bounce`
            + `count_outofband_bounce`
            + `count_soft_bounce`
            + `count_hard_bounce`
            + `count_block_bounce`
            + `count_admin_bounce`
            + `count_undetermined_bounce`
            + `count_delayed`
            + `count_delayed_first`
            + `count_rendered`
            + `count_unique_rendered`
            + `count_unique_confirmed_opened`
            + `count_clicked`
            + `count_unique_clicked`
            + `count_targeted`
            + `count_sent`
            + `count_accepted`
            + `count_spam_complaint`
            
  + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`
  + limit (optional, int, `5`) ... Maximum number of results to return
  + order_by (optional, string, `count_injected`) ... Metric by which to order results

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

  [Deliverability Metrics by Template][]


## Deliverability Metrics by Watched Domain [/metrics/deliverability/watched-domain{?from,to,domains,campaigns,templates,sandbox,metrics,timezone,limit,order_by}]

+ Model

    + Body

        ```
        {
          "results": [
            {
              "watched_domain": "aol.com",
              "count_targeted": 34432,
              "count_injected": 32323,
              "count_rejected": 2343,
              "count_sent": 34344
            },
            {
              "watched_domain": "gmail.com",
              "count_targeted": 34432,
              "count_injected": 32323,
              "count_rejected": 2343,
              "count_sent": 34344
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "count_accepted": {
                      "type":"number",
                      "required":false
                    },
                    "count_admin_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_block_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_failed": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_hard_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_inband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_injected": {
                      "type":"number",
                      "required":false
                    },
                    "count_outofband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_policy_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_rejected": {
                      "type":"number",
                      "required":false
                    },
                    "count_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "count_sent": {
                      "type":"number",
                      "required":false
                    },
                    "count_soft_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_spam_complaint": {
                      "type":"number",
                      "required":false
                    },
                    "count_targeted": {
                      "type":"number",
                      "required":false
                    },
                    "count_undetermined_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_confirmed_opened": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "total_delivery_time_first": {
                      "type":"number",
                      "required":false
                    },
                    "total_delivery_time_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "total_msg_volume": {
                      "type":"number",
                      "required":false
                    },
                    "watched_domain": {
                      "type":"string",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Deliverability Metrics by Watched Domain [GET]

Provides aggregate metrics grouped by watched domain over the time window specified. The difference
between domain and watched domain is that watched domains are comprised of the top 99% domains
in the world.

+ Parameters
    + from (required, datetime, `2014-07-11T08:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + to = `now` (optional, datetime, `2014-07-20T09:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + domains (optional, list, `gmail.com,yahoo.com,hotmail.com`) ... Comma-delimited list of domains to include
    + campaigns (optional, list, `Black Friday`) ... Comma-delimited list of campaigns to include
    + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
    + sandbox (optional, string, `true`) ... Restrict the query to events generated with a sandbox sending domain
    + metrics (required, list) ... Comma-delimited list of metrics for filtering
        + Values
            + `count_injected`
            + `count_bounce`
            + `count_rejected`
            + `count_delivered`
            + `count_delivered_first`
            + `count_delivered_subsequent`
            + `total_delivery_time_first`
            + `total_delivery_time_subsequent`
            + `total_msg_volume`
            + `count_policy_rejection`
            + `count_generation_rejection`
            + `count_generation_failed`
            + `count_inband_bounce`
            + `count_outofband_bounce`
            + `count_soft_bounce`
            + `count_hard_bounce`
            + `count_block_bounce`
            + `count_admin_bounce`
            + `count_undetermined_bounce`
            + `count_delayed`
            + `count_delayed_first`
            + `count_rendered`
            + `count_unique_rendered`
            + `count_unique_confirmed_opened`
            + `count_clicked`
            + `count_unique_clicked`
            + `count_targeted`
            + `count_sent`
            + `count_accepted`
            + `count_spam_complaint`
            
  + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`
  + limit (optional, int, `5`) ... Maximum number of results to return
  + order_by (optional, string, `count_injected`) ... Metric by which to order results

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

  [Deliverability Metrics by Watched Domain][]


## Time Series [/metrics/deliverability/time-series{?from,to,domains,campaigns,templates,sandbox,precision,metrics,timezone}]


+ Model

    + Body

        ```
        {
          "results": [
            {
              "ts": "2013-09-06T09:30",
              "count_targeted": 34432,
              "count_injected": 32323,
              "count_rejected": 2343,
              "count_sent": 34344,
              "count_delivered": 3434,
              "count_delivered_first": 343,
              "count_delivered_subsequent": 22323,
              "total_msg_volume": 33434,
              "count_inband_bounce": 2,
              "count_outofband_bounce": 2,
              "count_bounce": 2,
              "count_soft_bounce": 8,
              "count_hard_bounce": 6,
              "count_block_bounce": 4,
              "count_admin_bounce": 2,
              "count_undetermined_bounce": 2,
              "count_accepted": 3434,
              "count_delayed": 2,
              "count_generation_failed": 1,
              "count_generation_rejection": 1,
              "count_delayed_first": 5,
              "count_rendered": 111,
              "count_unique_rendered": 111,
              "count_unique_confirmed_opened": 111,
              "count_clicked": 8,
              "count_unique_clicked": 8,
              "count_spam_complaint": 5
            },
            {
              "ts": "2013-09-06T09:29",
              "count_targeted": 34432,
              "count_injected": 32323,
              "count_rejected": 2343,
              "count_sent": 34344,
              "count_delivered": 3434,
              "count_delivered_first": 343,
              "count_delivered_subsequent": 22323,
              "total_msg_volume": 33434,
              "count_inband_bounce": 2,
              "count_outofband_bounce": 2,
              "count_bounce": 2,
              "count_soft_bounce": 8,
              "count_hard_bounce": 6,
              "count_block_bounce": 4,
              "count_admin_bounce": 2,
              "count_undetermined_bounce": 2,
              "count_accepted": 3434,
              "count_delayed": 2,
              "count_generation_failed": 1,
              "count_generation_rejection": 1,
              "count_delayed_first": 5,
              "count_rendered": 111,
              "count_unique_rendered": 111,
              "count_unique_confirmed_opened": 111,
              "count_clicked": 8,
              "count_unique_clicked": 8,
              "count_spam_complaint": 7
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "count_accepted": {
                      "type":"number",
                      "required":false
                    },
                    "count_admin_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_block_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_failed": {
                      "type":"number",
                      "required":false
                    },
                    "count_generation_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_hard_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_inband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_injected": {
                      "type":"number",
                      "required":false
                    },
                    "count_outofband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_policy_rejection": {
                      "type":"number",
                      "required":false
                    },
                    "count_rejected": {
                      "type":"number",
                      "required":false
                    },
                    "count_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "count_sent": {
                      "type":"number",
                      "required":false
                    },
                    "count_soft_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_spam_complaint": {
                      "type":"number",
                      "required":false
                    },
                    "count_targeted": {
                      "type":"number",
                      "required":false
                    },
                    "count_undetermined_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_confirmed_opened": {
                      "type":"number",
                      "required":false
                    },
                    "count_unique_rendered": {
                      "type":"number",
                      "required":false
                    },
                    "total_delivery_time_first": {
                      "type":"number",
                      "required":false
                    },
                    "total_delivery_time_subsequent": {
                      "type":"number",
                      "required":false
                    },
                    "total_msg_volume": {
                      "type":"number",
                      "required":false
                    },
                    "ts": {
                      "type":"string",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Time-Series Metrics [GET]

Provides deliverability metrics ordered by a precision of time.

The following table describes the validation for the **precision** parameter:

| Value of         | Valid for time window of    |
|---------------|-------------|
|1min, 5min |day |
|hour |month |
|day, month |_any_ |

+ Parameters
    + from (required, datetime, `2014-07-11T07:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + to = `now` (optional, datetime, `2014-07-20T08:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + domains (optional, list `gmail.com,yahoo.com,hotmail.com`) ... Comma-delimited list of domains for filtering
    + campaigns (optional, list, `summerSale,promotionX`) ... Comma-delimited list of campaigns for filtering
    + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
    + sandbox (optional, string, `true`) ... Restrict the query to events generated with a sandbox sending domain
    + precision (optional, string, `day`) ... Precision of timeseries data returned

        + Values
            + `1min`
            + `5min`
            + `15min`
            + `hour`
            + `12hr`
            + `day`
            + `week`
            + `month`

    + metrics (required, list) ... Comma-delimited list of metrics for filtering
  
        + Values
            + `count_injected`
            + `count_bounce`
            + `count_rejected`
            + `count_delivered`
            + `count_delivered_first`
            + `count_delivered_subsequent`
            + `total_delivery_time_first`
            + `total_delivery_time_subsequent`
            + `total_msg_volume`
            + `count_policy_rejection`
            + `count_generation_rejection`
            + `count_generation_failed`
            + `count_inband_bounce`
            + `count_outofband_bounce`
            + `count_soft_bounce`
            + `count_hard_bounce`
            + `count_block_bounce`
            + `count_admin_bounce`
            + `count_undetermined_bounce`
            + `count_delayed`
            + `count_delayed_first`
            + `count_rendered`
            + `count_unique_rendered`
            + `count_unique_confirmed_opened`
            + `count_clicked`
            + `count_unique_clicked`
            + `count_targeted`
            + `count_sent`
            + `count_accepted`
            + `count_spam_complaint`

    + timezone = `UTC` (optional, string `America/New_York`) ... Standard timezone identification string, defaults to `UTC`

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

  [Time Series][]


## Bounce Reasons [/metrics/deliverability/bounce-reason{?from,to,domains,campaigns,templates,sandbox,metrics,timezone,limit}]

+ Model

    + Body

        ```
        {
          "results": [
            {
              "reason": "Some Fake Reason",
              "bounce_class_name": "Undetermined",
              "bounce_class_description": "The response text could not be identified",
              "bounce_category_id": 0,
              "bounce_category_name": "Undetermined",
              "classification_id": 1,
              "count_inband_bounce": 119,
              "count_outofband_bounce": 118,
              "count_bounce": 237
            },
            {
              "reason": "Some Fake Reason",
              "bounce_class_name": "Invalid Recipient",
              "bounce_class_description": "The recipient is invalid",
              "bounce_category_id": 1,
              "bounce_category_name": "Hard",
              "classification_id": 10,
              "count_inband_bounce": 133,
              "count_outofband_bounce": 126,
              "count_bounce": 259
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "bounce_category_name": {
                      "type":"string",
                      "required":false
                    },
                    "bounce_class_description": {
                      "type":"string",
                      "required":false
                    },
                    "bounce_class_name": {
                      "type":"string",
                      "required":false
                    },
                    "classification_id": {
                      "type":"number",
                      "required":false
                    },
                    "count_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_inband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_outofband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "reason": {
                      "type":"string",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Bounce Reason Metrics [GET]

Provides deliverability metrics, specific to bounce events, grouped by the bounce reasons.

+ Parameters
    + from (required, datetime, `2014-07-11T08:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + to = `now` (optional, datetime, `2014-07-20T09:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + domains (optional, list, `gmail.com,yahoo.com,hotmail.com`) ... Comma-delimited list of domains to include
    + campaigns (optional, list, `Black Friday`) ... Comma-delimited list of campaigns to include
    + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
    + sandbox (optional, string, `true`) ... Restrict the query to events generated with a sandbox sending domain
    + metrics (required, list) ... Comma-delimited list of metrics to include
        
        + Values
            + `count_bounce`
            + `count_inband_bounce`
            + `count_outofband_bounce`
            
    + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`
    + limit (optional, int, `5`) ... Maximum number of results to return [1,1000]

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

  [Bounce Reasons][]


## Bounce Classifications [/metrics/deliverability/bounce-classification{?from,to,domains,campaigns,templates,sandbox,metrics,timezone,limit}]

+ Model

    + Body

        ```
        {
          "results": [
            {
              "bounce_class_name": "Undetermined",
              "bounce_class_description": "The response text could not be identified",
              "bounce_category_name": "Undetermined",
              "count_bounce": 226,
              "count_inband_bounce": 205,
              "count_outofband_bounce": 21,
              "classification_id": 1
            },
            {
              "bounce_class_name": "Invalid Recipient",
              "bounce_class_description": "The recipient is invalid",
              "bounce_category_name": "Hard",
              "count_bounce": 249,
              "count_inband_bounce": 224,
              "count_outofband_bounce": 25,
              "classification_id": 10
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "bounce_category_name": {
                      "type":"string",
                      "required":false
                    },
                    "bounce_class_description": {
                      "type":"string",
                      "required":false
                    },
                    "bounce_class_name": {
                      "type":"string",
                      "required":false
                    },
                    "classification_id": {
                      "type":"number",
                      "required":false
                    },
                    "count_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_inband_bounce": {
                      "type":"number",
                      "required":false
                    },
                    "count_outofband_bounce": {
                      "type":"number",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Bounce Classification Metrics [GET]

Provides deliverability metrics, specific to bounce events, grouped by the bounce classification. (See [Bounce Classification Codes.](https://www.sparkpost.com/docs/bounce-classification-codes))

+ Parameters
    + from (required, datetime, `2014-07-11T08:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + to = `now` (optional, datetime, `2014-07-20T09:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + domains (optional, list, `gmail.com,yahoo.com,hotmail.com`) ... Comma-delimited list of domains to include
    + campaigns (optional, list, `Black Friday`) ... Comma-delimited list of campaigns to include
    + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
    + sandbox (optional, string, `true`) ... Restrict the query to events generated with a sandbox sending domain
    + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`
    + metrics (required, list) ... Comma-delimited list of metrics to include
        
        + Values
            + `count_bounce`
            + `count_inband_bounce`
            + `count_outofband_bounce`
            
    + limit (optional, int, `5`) ... Maximum number of results to return

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

  [Bounce Classifications][]


## Rejection Reasons [/metrics/deliverability/rejection-reason{?from,to,domains,campaigns,templates,sandbox,timezone,limit}]

+ Model

    + Body

        ```
        {
          "results": [
            {
              "reason": "520 rejection message",
              "count_rejected": 30,
              "rejection_category_id": 2,
              "rejection_type": "Generation Rejection"
            },
            {
              "reason": "503 rejection message",
              "count_rejected": 24,
              "rejection_category_id": 1,
              "rejection_type": "Policy Rejection"
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "count_rejected": {
                      "type":"number",
                      "required":false
                    },
                    "reason": {
                      "type":"string",
                      "required":false
                    },
                    "rejection_category_id": {
                      "type":"number",
                      "required":false
                    },
                    "rejection_category_name": {
                      "type":"string",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Rejection Reason Metrics [GET]

Provides deliverability metrics, specific to rejection events, grouped by the rejection reasons.

+ Parameters
  + from (required, datetime, `2014-07-11T08:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
  + to = `now` (optional, datetime, `2014-07-20T09:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
  + domains (optional, list, `gmail.com,yahoo.com,hotmail.com`) ... Comma-delimited list of domains to include
  + campaigns (optional, list, `Black Friday`) ... Comma-delimited list of campaigns to include
  
  + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
  + sandbox (optional, string, `true`) ... Restrict the query to events generated with a sandbox sending domain
  
  + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`
  + limit (optional, int, `5`) ... Maximum number of results to return

+ Response 200 (application/json)

  [Rejection Reasons][]


## Delay Reasons [/metrics/deliverability/delay-reason{?from,to,domains,campaigns,templates,sandbox,timezone,limit}]

+ Model

    + Body

        ```
        {
          "results":[
            {
              "reason": "400 fake tempfail reason",
              "count_delayed": 200,
              "count_delayed_first": 100
            },
            {
              "reason": "425 fake tempfail reason",
              "count_delayed": 100,
              "count_delayed_first": 50
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "count_delayed_first": {
                      "type":"number",
                      "required":false
                    },
                    "count_delayed": {
                      "type":"number",
                      "required":false
                    },
                    "reason": {
                      "type":"string",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Delay Reason Metrics [GET]

Provides deliverability metrics, specific to delay events, grouped by the delay reasons.

+ Parameters
  + from (required, datetime, `2014-07-11T08:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
  + to = `now` (optional, datetime, `2014-07-20T09:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
  + domains (optional, list, `gmail.com,yahoo.com,hotmail.com`) ... Comma-delimited list of domains to include
  + campaigns (optional, list, `Black Friday`) ... Comma-delimited list of campaigns to include
  
  + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
  + sandbox (optional, string, `true`) ... Restrict the query to events generated with a sandbox sending domain
  
  + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`
  + limit (optional, int, `5`) ... Maximum number of results to return

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

  [Delay Reasons][]


## Engagement Details [/metrics/deliverability/link-name{?from,to,timezone,campaigns,templates,metrics,limit}]

+ Model

    + Body

        ```
        {
          "results":[
            {
              "link_name": "top banner link",
              "count_clicked": 123,
              "count_raw_clicked": 456
            },
            {
              "link_name": "http://www.test.com/buy/our/stuff/now",
              "count_clicked": 123,
              "count_raw_clicked": 456
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "count_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "count_raw_clicked": {
                      "type":"number",
                      "required":false
                    },
                    "link_name": {
                      "type":"string",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Engagement Details [GET]

Provides deliverability metrics, specific to engagement events (clicks/opens), grouped by the link
name (or URL if no link name exists).

+ Parameters
    + from (required, datetime, `2014-07-11T09:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + to = `now` (optional, datetime, `2014-07-20T00:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
    + timezone = `UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`
    + metrics (required, list) ... Comma-delimited list of metrics to include
      
        + Values
            + `count_clicked`
            + `count_raw_clicked`
    
    + campaigns (optional, list, `Black Friday`) ... Comma-delimited list of campaigns to include
    + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
    + limit (optional, int, `5`) ... Maximum number of results to return

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

  [Engagement Details][]


## Deliveries By Attempt [/metrics/deliverability/attempt{?from,to,domains,campaigns,templates,sandbox,timezone}]

+ Model

    + Body

        ```
        {
          "results":[
            {
              "attempt": "1",
              "count_delivered": 100
            },
            {
              "attempt": "2",
              "count_delivered": 150
            }
          ]
        }
        ```

    + Schema

        ```
        {
          "type":"object",
          "$schema": "http://json-schema.org/draft-03/schema",
          "required":false,
          "properties":{
            "results": {
              "type":"array",
              "required":false,
              "items":
                {
                  "type":"object",
                  "required":false,
                  "properties":{
                    "attempt": {
                      "type":"number",
                      "required":false
                    },
                    "count_delivered": {
                      "type":"number",
                      "required":false
                    }
                  }
                }
            }
          }
        }
        ```

### Deliveries By Attempt [GET]

Provides aggregate count of deliveries grouped by the attempt number.

+ Parameters
  + from (required, datetime, `2014-07-11T08:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
  + to = `now` (optional, datetime, `2014-07-20T09:00`) ... Datetime in format of YYYY-MM-DDTHH:MM
  + domains (optional, list, `gmail.com,yahoo.com,hotmail.com`) ... Comma-delimited list of domains to include
  + campaigns (optional, list, `Black Friday`) ... Comma-delimited list of campaigns to include
  
  + templates (optional, list, `summer-sale`) ... Comma-delimited list of template IDs to include
  + sandbox (optional, string, `true`) ... Restrict the query to events generated with a sandbox sending domain
  
  + timezone =`UTC` (optional, string, `America/New_York`) ... Standard timezone identification string, defaults to `UTC`

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200 (application/json)

  [Deliveries By Attempt][]



## Campaigns List [/metrics/campaigns]

+ Model (application/json)

    + Body

        ```
        {
          "results": {
             "campaigns": [
               "Labor Day Sale",
               "New Year's Sale",
               "Founder's Day Event",
               "Winter Event",
               "Promotion X"
            ]
          }
        }
        ```

    + Schema

        ```
        {
          "type": "object",
          "required": true,
          "properties": {
            "results": {
              "type": "object",
              "required": true,
              "properties": {
                "campaigns": {
                  "type": "array",
                  "required": false
                }
              }
            }
          }
        }
        ```

### Campaigns List [GET]

Returns a list of campaigns that the Metrics API contains data on.

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200

  [Campaigns List][]


## Domains List [/metrics/domains]

+ Model (application/json)

    + Body

        ```
        {
          "results": {
             "domains": [
               "gmail.com",
               "yahoo.com",
               "msn.com",
               "aol.com",
               "hotmail.com"
            ]
          }
        }
        ```

    + Schema

        ```
        {
          "type": "object",
          "required": true,
          "properties": {
            "results": {
              "type": "object",
              "required": true,
              "properties": {
                "domains": {
                  "type": "array",
                  "required": false
                }
              }
            }
          }
        }
        ```

### Domains List [GET]

Returns a list of domains that the Metrics API contains data on.

+ Request

    + Headers

            Authorization: 14ac5499cfdd2bb2859e4476d2e5b1d2bad079bf
            Accept: application/json

+ Response 200

  [Domains List][]
