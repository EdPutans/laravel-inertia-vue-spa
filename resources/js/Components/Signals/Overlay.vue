<script lang="tsx" setup>
import 'bootstrap/dist/css/bootstrap.css';
import 'bootstrap/dist/js/bootstrap.js';
import { ref } from 'vue';
import Categories from './Categories.vue';
import SignalCustomisation from './SignalCustomisation.vue';
import SignalExplainer from './SignalExplainer.vue';
import SignalSelection from './SignalSelection.vue';

const sampleCats = {
  "App\\Signals\\Guests\\GuestSignalCategory": {
    "identifier": "App\\Signals\\AbstractSignalCategory",
    "name": "Guests",
    "icon": "fas fa-users",
    "description": "Signals related to guests.",
    "signals": [
      {
        "identifier": "App\\Signals\\Guests\\GuestAbandonedJourneySignal",
        "name": "Guest Abandoned Journey",
        "icon": "fas fa-user-times",
        "description": "This signal can be configured to check whether a guest has abandoned their journey. A guest is considered to have abandoned their journey\nwhen they have not interacted with the system for a specific period of time, having previously started a conversion journey.",
        "parameters": [
          {
            "identifier": "JourneyType",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "label": "Journey Type",
            "description": "The type of journey to check for.",
            "options": {
              "Booking": "Booking",
              "OrderAtTable": "Order At Table",
              "OwnChannelDelivery": "Own Channel Delivery",
              "ClickAndCollect": "Click And Collect",
              "GiftCards": "Gift Cards",
              "Registration": "Registration"
            },
            "required": true
          }
        ]
      },
      {
        "identifier": "App\\Signals\\Guests\\GuestAudienceSignal",
        "name": "Guest Audience",
        "icon": "fas fa-user-check",
        "description": "This signal can be configured to check whether a guest is part of a specific audience. An audience is a group of guests that share a common\ncharacteristic, such as having visited a specific location, having made a specific purchase, or having a specific demographic profile.",
        "parameters": [
          {
            "identifier": "AudienceRelation",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "label": "Audience Relation",
            "description": "The audience to check for.",
            "options": {
              "In": "In Audience",
              "NotIn": "Not In Audience"
            },
            "required": true
          },
          {
            "identifier": "AudienceIDs",
            "inputType": "App\\Signals\\Parameters\\Inputs\\ModelSelectionInput",
            "label": "Audience(s)",
            "description": "The audience(s) to check for.",
            "options": [],
            "required": true,
            "multiple": true
          }
        ]
      },
      {
        "identifier": "App\\Signals\\Guests\\GuestConsentSignal",
        "name": "Guest Consent",
        "icon": "fas fa-user-check",
        "description": "This signal can be configured to check whether a guest has given consent for a specific purpose. This can be used to check\nwhether a guest has given consent for a specific purpose, such as to receive emails, SMS or push notifications, or it\ncan be used to check whether a guest has given consent to all purposes.",
        "parameters": [
          {
            "identifier": "ConsentType",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "label": "Consent Type",
            "description": "The type of consent check to perform.",
            "options": {
              "Specific": "Specific",
              "All": "All"
            },
            "required": true
          },
          {
            "identifier": "SpecificConsent",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "label": "Specific Consent",
            "description": "The specific consent to check for.",
            "options": {
              "Email": "Email",
              "SMS": "SMS",
              "PushNotifications": "Push Notifications"
            },
            "display": "if:ConsentType,Specific",
            "validation": "required_if:ConsentType,Specific",
            "required": false
          },
          {
            "identifier": "ConsentStatus",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "label": "Consent Status",
            "description": "Whether the guest is required to have the consent or not.",
            "options": {
              "Present": "Present",
              "Missing": "Missing"
            },
            "required": true
          }
        ]
      },
      {
        "identifier": "App\\Signals\\Guests\\GuestIncentiveSignal",
        "name": "Guest Incentive",
        "icon": "fas fa-user-check",
        "description": "This signal can be configured to check whether a guest has an available incentive. An incentive is a reward, offer or voucher offered to a guest\nin exchange for a specific action, such as making a purchase, signing up to a newsletter, or visiting a specific location.",
        "parameters": [
          {
            "identifier": "IncentiveType",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "label": "Incentive Type",
            "description": "The incentive type to check for.",
            "options": {
              "Reward": "Reward",
              "Promotion": "Promotion",
              "Voucher": "Voucher"
            },
            "required": true
          }
        ]
      },
      {
        "identifier": "App\\Signals\\Guests\\GuestInfoSignal",
        "name": "Guest Info",
        "icon": "fas fa-user",
        "description": "This signal can be configured to check whether a specific piece of information is present for a guest. This can be used\nto check whether a guest has a specific piece of information, such as a phone number, email address, or any other\ninformation that we'd like to determine whether we have or not.",
        "parameters": [
          {
            "identifier": "InfoType",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "label": "Info Type",
            "description": "The type of information to check for.",
            "options": {
              "Registered": "Registered",
              "EmailAddress": "Email Address",
              "PhoneNumber": "Phone Number",
              "Address": "Address"
            },
            "required": true
          },
          {
            "identifier": "InfoStatus",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "label": "Info Status",
            "description": "Whether the guest is required to have the information or not.",
            "options": {
              "Present": "Present",
              "Missing": "Missing"
            },
            "required": true
          }
        ]
      },
      {
        "identifier": "App\\Signals\\Guests\\GuestKnownSignal",
        "name": "Guest Known",
        "icon": "fas fa-user-check",
        "description": "This signal can be configured to check whether a guest is known. A guest is known when they have been identified, by the system, as an\nidentifiable person.",
        "parameters": [
          {
            "identifier": "KnownStatus",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "label": "Known Status",
            "description": "Whether the guest is required to be known or not.",
            "options": {
              "true": "Known",
              "false": "Unknown"
            },
            "required": true,
            "cast": "boolean"
          }
        ]
      }
    ]
  },
  "App\\Signals\\Legacy\\LegacySignalCategory": {
    "identifier": "App\\Signals\\AbstractSignalCategory",
    "name": "Legacy",
    "icon": "fas fa-cogs",
    "description": "Legacy signals.",
    "signals": [
      {
        "identifier": "NumberOfHostOrPathVisits",
        "name": "Number of Visits",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "gt": "> Greater Than",
              "lt": "< Less Than",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "contains": "Contains",
              "starts_with": "Starts With",
              "ends_with": "Ends With",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          },
          {
            "identifier": "Value",
            "label": "Value",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Host or Path",
            "label": "Host or Path",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "host": "Host",
              "path": "Path"
            },
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "IsOnPath",
        "name": "Is On Path",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Path",
            "label": "Path",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          }
        ]
      },
      {
        "identifier": "IsOnDomain",
        "name": "Is On Domain",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Path",
            "label": "Path",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "IsDayOfWeek",
        "name": "Is Day Of Week",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Day of Week",
            "label": "Day of Week",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "1": "Monday",
              "2": "Tuesday",
              "3": "Wednesday",
              "4": "Thursday",
              "5": "Friday",
              "6": "Saturday",
              "7": "Sunday"
            },
            "multiple": false,
            "required": true
          }
        ]
      },
      {
        "identifier": "HasNotSeenPath",
        "name": "Has Not Seen Path",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Path",
            "label": "Path",
            "inputType": "App\\Signals\\Parameters\\Inputs\\RepeaterInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasSeenPath",
        "name": "Has Seen Path",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Path",
            "label": "Path",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          }
        ]
      },
      {
        "identifier": "HasSeenPageHash",
        "name": "Has Seen Page Hash",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          },
          {
            "identifier": "Path",
            "label": "Path",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasNotSeenPageHash",
        "name": "Has Not Seen Page Hash",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          },
          {
            "identifier": "Path",
            "label": "Path",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasSeenPageParameter",
        "name": "Has Seen Page Parameter",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Parameter",
            "label": "Parameter",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          },
          {
            "identifier": "Value",
            "label": "Value",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasSeenPageParameterWithinTimeFrame",
        "name": "Has Seen Page Parameter Within Timeframe",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Parameter",
            "label": "Parameter",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          },
          {
            "identifier": "Value",
            "label": "Value",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Within last X days",
            "label": "Within last X days",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasSeenPageParameterOutsideTimeFrame",
        "name": "Has Seen Page Parameter Outside Timeframe",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Parameter",
            "label": "Parameter",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          },
          {
            "identifier": "Value",
            "label": "Value",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "More than X days ago",
            "label": "More than X days ago",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasNotSeenPageParameter",
        "name": "Has Not Seen Page Parameter",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Parameter",
            "label": "Parameter",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          },
          {
            "identifier": "Value",
            "label": "Value",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasSeenPageUTM",
        "name": "Has Seen Page UTM",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "UTM",
            "label": "UTM",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "source": "utm_source",
              "medium": "utm_medium",
              "campaign": "utm_campaign",
              "term": "utm_term",
              "content": "utm_content"
            },
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          },
          {
            "identifier": "Value",
            "label": "Value",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasNotSeenPageUTM",
        "name": "Has Not Seen Page UTM",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "UTM",
            "label": "UTM",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "source": "utm_source",
              "medium": "utm_medium",
              "campaign": "utm_campaign",
              "term": "utm_term",
              "content": "utm_content"
            },
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          },
          {
            "identifier": "Value",
            "label": "Value",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "NumberOfPageviews",
        "name": "Number of Pageviews",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "gt": "> Greater Than",
              "lt": "< Less Than",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "contains": "Contains",
              "starts_with": "Starts With",
              "ends_with": "Ends With",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          },
          {
            "identifier": "Value",
            "label": "Value",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasNotSeenDOMElement",
        "name": "Has Not Seen DOM Element",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "CSS Element Selector",
            "label": "CSS Element Selector",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Path",
            "label": "Path",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          }
        ]
      },
      {
        "identifier": "HasClickedButton",
        "name": "Has Clicked Button",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "CSS Element Selector",
            "label": "CSS Element Selector",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Path",
            "label": "Path",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          }
        ]
      },
      {
        "identifier": "CanSeeElementOnPage",
        "name": "Can See Element On Page",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "CSS Element Selector",
            "label": "CSS Element Selector",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Path",
            "label": "Path",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "Comparator",
            "label": "Comparator",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "starts_with": "Starts With",
              "contains": "Contains",
              "ends_with": "Ends With",
              "eq": "= Exactly",
              "neq": "!= Doesn't Match",
              "exists": "Exists"
            },
            "multiple": false,
            "required": true
          }
        ]
      },
      {
        "identifier": "HasNotSeenCampaign",
        "name": "Has Not Seen A Campaign",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Campaign ID",
            "label": "Campaign ID",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "In Last \"n\" days",
            "label": "In Last \"n\" days",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasSeenCampaign",
        "name": "Has Seen A Campaign",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Campaign ID",
            "label": "Campaign ID",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "In Last \"n\" days",
            "label": "In Last \"n\" days",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasSeenCampaignVariant",
        "name": "Has Seen A Campaign Variant",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Campaign Variant ID",
            "label": "Campaign Variant ID",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "In Last \"n\" days",
            "label": "In Last \"n\" days",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "HasNotConverted",
        "name": "Has Not Matched a Conversion Tracker",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Tracker ID",
            "label": "Tracker ID",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "In Last \"n\" days",
            "label": "In Last \"n\" days",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "PreviouslySeenATriggerBeforeXTimes",
        "name": "Previously seen a trigger before X times",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Trigger ID",
            "label": "Trigger ID",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          },
          {
            "identifier": "DateTime",
            "label": "DateTime",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "IsLoggedIn",
        "name": "Is Logged In",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Is Visitor Logged In?",
            "label": "Is Visitor Logged In?",
            "inputType": "App\\Signals\\Parameters\\Inputs\\BooleanInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "IsRegistered",
        "name": "Is Registered",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Is The Visitor Registered?",
            "label": "Is The Visitor Registered?",
            "inputType": "App\\Signals\\Parameters\\Inputs\\BooleanInput",
            "options": "",
            "multiple": false,
            "required": false
          }
        ]
      },
      {
        "identifier": "IsOnDevice",
        "name": "Visitor Is On A Specific Device Type",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Device Type",
            "label": "Device Type",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "mobile": "Mobile",
              "desktop": "Desktop",
              "tablet": "Tablet"
            },
            "multiple": true,
            "required": false
          }
        ]
      },
      {
        "identifier": "IsTester",
        "name": "The visitor is in the `Tester` cohort",
        "icon": "",
        "description": "",
        "parameters": []
      },
      {
        "identifier": "GuestIncentiveStatus",
        "name": "Guest Incentive Status",
        "icon": "",
        "description": "",
        "parameters": [
          {
            "identifier": "Incentive Type",
            "label": "Incentive Type",
            "inputType": "App\\Signals\\Parameters\\Inputs\\SelectInput",
            "options": {
              "Reward": "Reward",
              "Promotion": "Promotion",
              "Voucher": "Voucher"
            },
            "multiple": false,
            "required": true
          },
          {
            "identifier": "Expiration Threshold Days",
            "label": "Expiration Threshold Days",
            "inputType": "App\\Signals\\Parameters\\Inputs\\TextInput",
            "options": "",
            "multiple": false,
            "required": true
          }
        ]
      }
    ],
    "legacy": true
  }
}

defineProps({
  onSubmit: Function,
  onClose: Function,
});


const categories = ref(sampleCats);
const selectedCategory = ref(categories.value['App\\Signals\\Guests\\GuestSignalCategory']);

const hoveredOverSignal = ref(undefined);
const hoveredOverCategory = ref(undefined);
const selectedSignal = ref(undefined);

const appliedCustomisations = ref();

const setHoveredOverSignal = (signal) => {
  hoveredOverSignal.value = signal;
};
const setHoveredCategorySignal = (category) => {
  hoveredOverCategory.value = category;
};
const setSelectedSignal = (signal) => {
  hoveredOverSignal.value = signal;
  selectedSignal.value = signal;
};

const resetSelectedSignal = () => {
  selectedSignal.value = undefined;
  hoveredOverSignal.value = undefined;
};

const setSelectedCategory = (category) => {
  hoveredOverSignal.value = undefined;
  selectedCategory.value = category;
};

const open = ref(true);

const getExplainerValue = () => {
  if (hoveredOverSignal.value) return hoveredOverSignal.value;
  if (selectedSignal.value) return selectedSignal.value;

  return undefined;
};
const shouldShowExplainer = () => !!getExplainerValue();

function toggle() {
  open.value = !open.value
}
</script>


<template>
  <div v-if="open" class="modal fade modal-xl show" tabindex="-1" role="dialog" style="display: block;">
    <div class="modal-dialog modal-xl" role="document">
      <div class="modal-content">
        <div class="modal-header d-flex justify-content-between" style="border-bottom: none;">
          <div class="d-flex align-items-center ">
            <h5 class="modal-title">Configure Signal</h5>
          </div>
          <button type="button" class="close bg-white border-0" aria-label="Close" :on-click="toggle">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <div class="container">
            <div class="row">
              <div class="col border-top-0 border-left-0 border-bottom-0">
                <Categories v-if="!selectedSignal" :selectedCategory="selectedCategory" :categories="categories"
                  :setSelectedCategory="setSelectedCategory" :hoveredOverCategory="hoveredOverCategory"
                  :setHoveredCategorySignal="setHoveredCategorySignal" />

                <div v-else>
                  <SignalSelection :selectedCategory="selectedCategory" :hoveredOverSignal="hoveredOverSignal"
                    :setHoveredOverSignal="setHoveredOverSignal" :selectedSignal="selectedSignal"
                    :setSelectedSignal="setSelectedSignal" />
                </div>

              </div>
              <div class="col border border-top-0 border-left-0 border-bottom-0">
                <SignalSelection v-if="!selectedSignal" :selectedCategory="selectedCategory"
                  :hoveredOverSignal="hoveredOverSignal" :setHoveredOverSignal="setHoveredOverSignal"
                  :selectedSignal="selectedSignal" :setSelectedSignal="setSelectedSignal" />
                <SignalCustomisation v-else :selectedSignal="selectedSignal"
                  :appliedCustomisations="appliedCustomisations" />
              </div>
              <div class="col">
                <SignalExplainer v-if="shouldShowExplainer()" :signal="getExplainerValue()" />
              </div>
            </div>
          </div>
        </div>
        <div class="modal-footer" style="border-top: none;">
          <button type="button" class="btn btn-primary" v-on:click="$props.onSubmit">Save changes</button>
          <button type="button" class="btn btn-secondary" v-on:click="toggle">Close</button>
        </div>
      </div>
    </div>
  </div>
</template>
