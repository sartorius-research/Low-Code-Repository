# Low-Code-Repository
### Repository of Node-RED Low-Code Use Cases

## 1. Online model deployment and integration into a SCADA system <br>
![image](<img width="1440" height="480" alt="image" src="https://github.com/user-attachments/assets/a802d055-2e46-4a17-b6ee-e979a22c6d81" />

)

This JSON configuration defines a workflow that retrieves spectroscopy data, processes it through a predictive model, and publishes the model results to an OPC UA server, which can then be accessed by a SCADA system.

The setup uses the **[BioPAT® Viamass dielectric spectroscopy probe](https://shop.sartorius.com/de/p/biopatviamass/BioPAT_Viamass)** in combination with the **BioPAT® Viamass Connect Hub** to collect spectroscopy data. The resulting model output is integrated into **[BioPAT® MFCS 4.13](https://www.sartorius.com/en/products/process-analytical-technology/process-control-automation/biobrain-supervise?utm_source=google&utm_medium=cpc&utm_campaign=ww_en_search_PI-Boost_BioPAT-MFCS&gad_source=1&gad_campaignid=10692165010&gclid=Cj0KCQjw4qHEBhCDARIsALYKFNOScObdCQbfh6pU2o4N_CMV3_WFoXDLJhQp0VoiOesVicRQOsTTdIsaAmSDEALw_wcB)** via its **OPC UA client feature**.


```json
[
    {
        "id": "8d134948e9e90563",
        "type": "group",
        "z": "54683189a563b4b1",
        "name": "Read Data",
        "style": {
            "label": true
        },
        "nodes": [
            "86ce3655a71bd54a",
            "f93a2e6e9baa3255",
            "a5e9c11330d3b998"
        ],
        "x": 394,
        "y": 219,
        "w": 652,
        "h": 142
    },
    {
        "id": "86ce3655a71bd54a",
        "type": "OpcUa-Item",
        "z": "54683189a563b4b1",
        "g": "8d134948e9e90563",
        "item": "ns=5;s=\\\\.\\Futura 02\\Zeroed Averaged Capacitance Values",
        "datatype": "Float Array",
        "value": "",
        "name": "Zeroed Averaged Capacitance values",
        "x": 570,
        "y": 320,
        "wires": [
            [
                "a5e9c11330d3b998"
            ]
        ]
    },
    {
        "id": "f93a2e6e9baa3255",
        "type": "comment",
        "z": "54683189a563b4b1",
        "g": "8d134948e9e90563",
        "name": "",
        "info": "Receiving Spectroscopy Raw Data from OPC UA Server",
        "x": 480,
        "y": 260,
        "wires": []
    },
    {
        "id": "a5e9c11330d3b998",
        "type": "OpcUa-Client",
        "z": "54683189a563b4b1",
        "g": "8d134948e9e90563",
        "endpoint": "afc2f353b73c1625",
        "action": "read",
        "deadbandtype": "a",
        "deadbandvalue": 1,
        "time": 10,
        "timeUnit": "s",
        "certificate": "n",
        "localfile": "",
        "localkeyfile": "",
        "securitymode": "None",
        "securitypolicy": "None",
        "folderName4PKI": "",
        "name": "OPC UA Client for Viamass",
        "x": 900,
        "y": 320,
        "wires": [
            [
                "fdbdf326d02dae13"
            ]
        ]
    },
    {
        "id": "afc2f353b73c1625",
        "type": "OpcUa-Endpoint",
        "endpoint": "opc.tcp://localhost:53882/",
        "secpol": "None",
        "secmode": "None",
        "none": false,
        "login": false,
        "usercert": false,
        "usercertificate": "",
        "userprivatekey": ""
    },
    {
        "id": "f8d589616abe9ecd",
        "type": "group",
        "z": "54683189a563b4b1",
        "name": "Process Data",
        "style": {
            "label": true
        },
        "nodes": [
            "fdbdf326d02dae13"
        ],
        "x": 1074,
        "y": 279,
        "w": 252,
        "h": 82
    },
    {
        "id": "fdbdf326d02dae13",
        "type": "function",
        "z": "54683189a563b4b1",
        "g": "f8d589616abe9ecd",
        "name": "Spectroscopy Model",
        "func": "msg.payload = -1.11411+msg.payload[0]*-0.0846305+msg.payload[1]*-0.0693173+msg.payload[2]*-0.0509203+msg.payload[3]*-0.0266838+msg.payload[4]*-0.00368787+msg.payload[5]*0.0244135+msg.payload[6]*0.0543474+msg.payload[7]*0.0815575+msg.payload[8]*0.100042+msg.payload[9]*0.109601+msg.payload[10]*0.107292+msg.payload[11]*0.0949137+msg.payload[12]*0.0787177+msg.payload[13]*0.0704221+msg.payload[14]*0.0454615+msg.payload[15]*0.0338642+msg.payload[16]*0.0239638+msg.payload[17]*0.0169988+msg.payload[18]*0.0131833+msg.payload[19]*0.00917408+msg.payload[20]*0.00747873+msg.payload[21]*0.00519937+msg.payload[22]*0.00307098+msg.payload[23]*0.00225113+msg.payload[24]*0.00143756\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 1200,
        "y": 320,
        "wires": [
            [
                "ecb42cf9b37451bf"
            ]
        ]
    },
    {
        "id": "51aae4e9f4f81bda",
        "type": "group",
        "z": "54683189a563b4b1",
        "name": "Write Data",
        "style": {
            "label": true
        },
        "nodes": [
            "ecb42cf9b37451bf",
            "a65d9f5dd6f30b03",
            "67cd2dd521a49f6e"
        ],
        "x": 1344,
        "y": 219,
        "w": 402,
        "h": 142
    },
    {
        "id": "ecb42cf9b37451bf",
        "type": "OpcUa-Item",
        "z": "54683189a563b4b1",
        "g": "51aae4e9f4f81bda",
        "item": "ns=1;s=viamass-VCC",
        "datatype": "Double",
        "value": "",
        "name": "viamass-VCC",
        "x": 1450,
        "y": 320,
        "wires": [
            [
                "a65d9f5dd6f30b03"
            ]
        ]
    },
    {
        "id": "a65d9f5dd6f30b03",
        "type": "OpcUa-Client",
        "z": "54683189a563b4b1",
        "g": "51aae4e9f4f81bda",
        "endpoint": "afc2f353b73c1625",
        "action": "write",
        "deadbandtype": "a",
        "deadbandvalue": 1,
        "time": 10,
        "timeUnit": "s",
        "certificate": "n",
        "localfile": "",
        "localkeyfile": "",
        "securitymode": "None",
        "securitypolicy": "None",
        "folderName4PKI": "",
        "name": "",
        "x": 1640,
        "y": 320,
        "wires": [
            []
        ]
    },
    {
        "id": "67cd2dd521a49f6e",
        "type": "comment",
        "z": "54683189a563b4b1",
        "g": "51aae4e9f4f81bda",
        "name": "",
        "info": "OPC UA Node ID that is receiving the model outcome and can be accessed by SCADA system.",
        "x": 1430,
        "y": 260,
        "wires": []
    },
    {
        "id": "cbe5c6e01e0f5bae",
        "type": "group",
        "z": "54683189a563b4b1",
        "name": "Server",
        "style": {
            "label": true
        },
        "nodes": [
            "4bb1da24c6e28510",
            "49e1b80836fc1f7d",
            "05e83eef11cdf9dc"
        ],
        "x": 394,
        "y": 419,
        "w": 572,
        "h": 142
    },
    {
        "id": "4bb1da24c6e28510",
        "type": "inject",
        "z": "54683189a563b4b1",
        "g": "cbe5c6e01e0f5bae",
        "name": "AddVariable=viamass-VCC",
        "props": [
            {
                "p": "payload"
            },
            {
                "p": "topic",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": true,
        "onceDelay": "10",
        "topic": "ns=1;s=viamass-VCC;datatype=Double",
        "payload": "{\"opcuaCommand\":\"addVariable\"}",
        "payloadType": "json",
        "x": 560,
        "y": 520,
        "wires": [
            [
                "49e1b80836fc1f7d"
            ]
        ]
    },
    {
        "id": "49e1b80836fc1f7d",
        "type": "OpcUa-Server",
        "z": "54683189a563b4b1",
        "g": "cbe5c6e01e0f5bae",
        "port": "53883",
        "name": "LocalViamassServer",
        "endpoint": "",
        "users": "users.json",
        "nodesetDir": "",
        "autoAcceptUnknownCertificate": true,
        "registerToDiscovery": false,
        "constructDefaultAddressSpace": true,
        "allowAnonymous": true,
        "endpointNone": true,
        "endpointSign": false,
        "endpointSignEncrypt": false,
        "endpointBasic128Rsa15": false,
        "endpointBasic256": false,
        "endpointBasic256Sha256": false,
        "maxNodesPerBrowse": 0,
        "maxNodesPerHistoryReadData": 0,
        "maxNodesPerHistoryReadEvents": 0,
        "maxNodesPerHistoryUpdateData": 0,
        "maxNodesPerRead": 0,
        "maxNodesPerWrite": 0,
        "maxNodesPerMethodCall": 0,
        "maxNodesPerRegisterNodes": 0,
        "maxNodesPerNodeManagement": 0,
        "maxMonitoredItemsPerCall": 0,
        "maxNodesPerHistoryUpdateEvents": 0,
        "maxNodesPerTranslateBrowsePathsToNodeIds": 0,
        "maxConnectionsPerEndpoint": 20,
        "maxMessageSize": 4096,
        "maxBufferSize": 4096,
        "x": 840,
        "y": 520,
        "wires": [
            []
        ]
    },
    {
        "id": "05e83eef11cdf9dc",
        "type": "comment",
        "z": "54683189a563b4b1",
        "g": "cbe5c6e01e0f5bae",
        "name": "",
        "info": "OPC UA Server that is initiated to offer the outcome of the model",
        "x": 480,
        "y": 460,
        "wires": []
    }
]

```

## 2. Data Dashboarding and Monitoring <br>
![image](https://github.com/user-attachments/assets/f44c8e13-cd7e-4376-ac8a-69bd8e4a6495)

This JSON represents a Node-RED flow designed to ingest spectral data, process it through a model, and visualize the results in real-time using a charting module. Additionally, when the viable cell concentration reaches a critical threshold, the system marks this point on the plot and triggers a notification. This notification is sent via a Telegram bot, which can be accessed through a desktop application or a smartphone app. To ensure proper functionality, IP addresses, Telegram chat IDs, bot credentials, and bot tokens must be generated and configured individually.

```json
[
    {
        "id": "2a3fe95c7aff5777",
        "type": "function",
        "z": "80071d512ef251f7",
        "name": "VCC Value Check and Forward",
        "func": "// Initialize context variable if not set\nif (context.get(\"vccAlarmTriggered\") === undefined) {\n    context.set(\"vccAlarmTriggered\", false);\n}\n\n// Check if reset toggle is triggered\nif (msg.topic === \"reset\") {\n    context.set(\"vccAlarmTriggered\", false);\n    node.status({ fill: \"green\", shape: \"dot\", text: \"Ready\" });\n    return null; // Do not send a message on reset\n}\n\n// Get the incoming value\nlet value = parseFloat(msg.payload);\n\n// If value is >= 1.27 and first time triggering, send alarm\nif (value >= 1.27 && !context.get(\"vccAlarmTriggered\")) {\n    context.set(\"vccAlarmTriggered\", true);\n    node.status({ fill: \"red\", shape: \"dot\", text: \"VCC Alarm Sent\" });\n\n    return { \n        topic: \"VCC ALARM\",\n        payload: value \n    };\n}\n\nreturn null; // No message sent if conditions aren't met\n",
        "outputs": 1,
        "timeout": 0,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 1130,
        "y": 360,
        "wires": [
            [
                "929b46d6898a5506"
            ]
        ]
    },
    {
        "id": "6cc846bd92d34fe9",
        "type": "change",
        "z": "80071d512ef251f7",
        "name": "",
        "rules": [
            {
                "t": "set",
                "p": "topic",
                "pt": "msg",
                "to": "VCC in 10^6/mL",
                "tot": "str"
            }
        ],
        "action": "",
        "property": "",
        "from": "",
        "to": "",
        "reg": false,
        "x": 1330,
        "y": 240,
        "wires": [
            [
                "929b46d6898a5506"
            ]
        ]
    },
    {
        "id": "929b46d6898a5506",
        "type": "ui_chart",
        "z": "80071d512ef251f7",
        "name": "VCC",
        "group": "ba3716afe03659de",
        "order": 12,
        "width": 0,
        "height": 0,
        "label": "VCC",
        "chartType": "line",
        "legend": "true",
        "xformat": "HH:mm:ss",
        "interpolate": "linear",
        "nodata": "",
        "dot": false,
        "ymin": "0",
        "ymax": "5",
        "removeOlder": "2",
        "removeOlderPoints": "",
        "removeOlderUnit": "86400",
        "cutout": 0,
        "useOneColor": false,
        "useUTC": false,
        "colors": [
            "#1f77b4",
            "#ff0000",
            "#ff7f0e",
            "#2ca02c",
            "#98df8a",
            "#d62728",
            "#ff9896",
            "#9467bd",
            "#c5b0d5"
        ],
        "outputs": 1,
        "useDifferentColor": false,
        "className": "",
        "x": 1610,
        "y": 240,
        "wires": [
            []
        ]
    },
    {
        "id": "85f34e52c6776262",
        "type": "function",
        "z": "80071d512ef251f7",
        "name": "VCC Critical Check",
        "func": "// Initialize context variable if not set\nif (context.get(\"alertTriggered\") === undefined) {\n    context.set(\"alertTriggered\", false);\n}\n\n// Check if reset toggle is triggered\nif (msg.topic === \"reset\") {\n    context.set(\"alertTriggered\", false);\n    node.status({ fill: \"green\", shape: \"dot\", text: \"Ready\" });\n    return null; // Do not send a message on reset\n}\n\n// Get the incoming value\nlet value = parseFloat(msg.payload);\n\n// If value is >= 1.27 and first time triggering, send alert\nif (value >= 1.27 && !context.get(\"alertTriggered\")) {\n    context.set(\"alertTriggered\", true);\n    node.status({ fill: \"red\", shape: \"dot\", text: \"Alert Sent\" });\n\n    return { payload: \"VCC has reached critical value!\" };\n}\n\nreturn null; // No message sent if conditions aren't met",
        "outputs": 1,
        "timeout": "",
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 1090,
        "y": 120,
        "wires": [
            [
                "c47377babf2d43a3"
            ]
        ]
    },
    {
        "id": "c47377babf2d43a3",
        "type": "function",
        "z": "80071d512ef251f7",
        "name": "Wrapper for Telegram JSON",
        "func": "msg.payload = {\n    \"chatId\": \"\",\n    \"type\": \"message\",\n    \"content\": msg.payload\n};\n\nreturn msg;\n",
        "outputs": 1,
        "timeout": 0,
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 1380,
        "y": 120,
        "wires": [
            [
                "f30e1fd5ddc43af4"
            ]
        ]
    },
    {
        "id": "e764de0ac0d0e3f2",
        "type": "inject",
        "z": "80071d512ef251f7",
        "name": "Reset Chart",
        "props": [
            {
                "p": "payload",
                "v": "clear",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "topic": "",
        "x": 810,
        "y": 420,
        "wires": [
            [
                "94d503efb8aea83b"
            ]
        ]
    },
    {
        "id": "94d503efb8aea83b",
        "type": "function",
        "z": "80071d512ef251f7",
        "name": "Clear Chart Data",
        "func": "msg.payload = [];\nmsg.topic = \"clear\";\nreturn msg;",
        "outputs": 1,
        "noerr": 0,
        "x": 1170,
        "y": 420,
        "wires": [
            [
                "929b46d6898a5506"
            ]
        ]
    },
    {
        "id": "f30e1fd5ddc43af4",
        "type": "telegram sender",
        "z": "80071d512ef251f7",
        "name": "VCC BOT",
        "bot": "8d979fa4b5aa89d9",
        "haserroroutput": false,
        "outputs": 1,
        "x": 1620,
        "y": 120,
        "wires": [
            []
        ]
    },
    {
        "id": "958a4e358ffbd523",
        "type": "inject",
        "z": "80071d512ef251f7",
        "name": "Reset Checker",
        "props": [
            {
                "p": "topic",
                "v": "reset",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "reset",
        "x": 800,
        "y": 120,
        "wires": [
            [
                "85f34e52c6776262"
            ]
        ]
    },
    {
        "id": "4bbcf1b26185912a",
        "type": "inject",
        "z": "80071d512ef251f7",
        "name": "Reset Alarm",
        "props": [
            {
                "p": "topic",
                "v": "reset",
                "vt": "str"
            }
        ],
        "repeat": "",
        "crontab": "",
        "once": false,
        "onceDelay": 0.1,
        "topic": "reset",
        "x": 810,
        "y": 360,
        "wires": [
            [
                "2a3fe95c7aff5777"
            ]
        ]
    },
    {
        "id": "f3c2ae50170a4098",
        "type": "OpcUa-Item",
        "z": "80071d512ef251f7",
        "item": "ns=5;s=\\\\.\\Futura 01\\Zeroed Averaged Capacitance Values",
        "datatype": "Float Array",
        "value": "",
        "name": "Zeroed Averaged Capacitance values",
        "x": 410,
        "y": 240,
        "wires": [
            [
                "842606fd8ee1ded8"
            ]
        ]
    },
    {
        "id": "842606fd8ee1ded8",
        "type": "OpcUa-Client",
        "z": "80071d512ef251f7",
        "endpoint": "4f3a5d493bf11d53",
        "action": "read",
        "deadbandtype": "a",
        "deadbandvalue": 1,
        "time": 10,
        "timeUnit": "s",
        "certificate": "n",
        "localfile": "",
        "localkeyfile": "",
        "securitymode": "None",
        "securitypolicy": "None",
        "useTransport": false,
        "maxChunkCount": "",
        "maxMessageSize": "",
        "receiveBufferSize": "",
        "sendBufferSize": "",
        "name": "OPC UA Client for Viamass",
        "x": 750,
        "y": 240,
        "wires": [
            [
                "ab9a7ce6017a08a6"
            ],
            []
        ]
    },
    {
        "id": "ab9a7ce6017a08a6",
        "type": "function",
        "z": "80071d512ef251f7",
        "name": "Viamass AAV Model",
        "func": "msg.payload = 0.160221 +\n              msg.payload[0] * 0.0212904 +\n              msg.payload[1] * -0.00466832 +\n              msg.payload[2] * -0.0124438 +\n              msg.payload[3] * -0.0283811 +\n              msg.payload[4] * -0.0200389 +\n              msg.payload[5] * -0.0146749 +\n              msg.payload[6] * 0.000626439 +\n              msg.payload[7] * 0.0163565 +\n              msg.payload[8] * 0.0316 +\n              msg.payload[9] * 0.0389127 +\n              msg.payload[10] * 0.0425114 +\n              msg.payload[11] * 0.0473631 +\n              msg.payload[12] * 0.0426975 +\n              msg.payload[13] * 0.0410814 +\n              msg.payload[14] * 0.0284757 +\n              msg.payload[15] * 0.0215087 +\n              msg.payload[16] * 0.01413 +\n              msg.payload[17] * 0.00852811 +\n              msg.payload[18] * 0.00654028 +\n              msg.payload[19] * 0.00510798 +\n              msg.payload[20] * 0.00379282 +\n              msg.payload[21] * 0.00139237 +\n              msg.payload[22] * 0.00225059 +\n              msg.payload[23] * 0.00472966 +\n              msg.payload[24] * 0.00268755;\nreturn msg;\n",
        "outputs": 1,
        "timeout": "",
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 1040,
        "y": 240,
        "wires": [
            [
                "85f34e52c6776262",
                "2a3fe95c7aff5777",
                "6cc846bd92d34fe9"
            ]
        ]
    },
    {
        "id": "58f804106deed2e7",
        "type": "comment",
        "z": "80071d512ef251f7",
        "name": "",
        "info": "OPC UA Client to access Viamass spectral data.",
        "x": 320,
        "y": 280,
        "wires": []
    },
    {
        "id": "b54aac63f386d2cd",
        "type": "comment",
        "z": "80071d512ef251f7",
        "name": "",
        "info": "OPC UA Client to access Viamass spectral data.",
        "x": 1000,
        "y": 280,
        "wires": []
    },
    {
        "id": "d42d127106f49199",
        "type": "comment",
        "z": "80071d512ef251f7",
        "name": "",
        "info": "Toggles to reset Cart data and to reset Value checker for Charting, once critical value has been reached.",
        "x": 800,
        "y": 460,
        "wires": []
    },
    {
        "id": "882ef873d9ea84f2",
        "type": "comment",
        "z": "80071d512ef251f7",
        "name": "",
        "info": "Toggle to set back the VCC Critical Check component that forwards to the Telegram Bot in case a critical VCC is reached.",
        "x": 820,
        "y": 160,
        "wires": []
    },
    {
        "id": "1f46e1773eadd505",
        "type": "comment",
        "z": "80071d512ef251f7",
        "name": "",
        "info": "Wrapper to put the incoming msg.payload into the appropriate format for the Telegram Bot",
        "x": 1320,
        "y": 160,
        "wires": []
    },
    {
        "id": "ba3716afe03659de",
        "type": "ui_group",
        "name": "VCC",
        "tab": "c522230dc8e805ee",
        "order": 1,
        "disp": true,
        "width": "6",
        "collapse": false,
        "className": ""
    },
    {
        "id": "8d979fa4b5aa89d9",
        "type": "telegram bot",
        "botname": "vcconline_bot",
        "usernames": "",
        "chatids": "",
        "baseapiurl": "",
        "testenvironment": false,
        "updatemode": "polling",
        "addressfamily": "4",
        "pollinterval": "300",
        "usesocks": false,
        "sockshost": "",
        "socksprotocol": "socks5",
        "socksport": "6667",
        "socksusername": "anonymous",
        "sockspassword": "",
        "bothost": "",
        "botpath": "",
        "localbothost": "0.0.0.0",
        "localbotport": "8443",
        "publicbotport": "8443",
        "privatekey": "",
        "certificate": "",
        "useselfsignedcertificate": false,
        "sslterminated": false,
        "verboselogging": false
    },
    {
        "id": "4f3a5d493bf11d53",
        "type": "OpcUa-Endpoint",
        "endpoint": "opc.tcp://10.226.74.15:48050",
        "secpol": "None",
        "secmode": "None",
        "none": false,
        "login": false,
        "usercert": false,
        "usercertificate": "",
        "userprivatekey": ""
    },
    {
        "id": "c522230dc8e805ee",
        "type": "ui_tab",
        "name": "Dashboarding & Monitoring",
        "icon": "dashboard",
        "order": 3,
        "disabled": false,
        "hidden": false
    }
]
```
## 3. Interfacing of Equipment and Flow Control Automation for Multi-Column Chromatography Systems <br>

![image](https://github.com/user-attachments/assets/27f385ce-9697-4b5a-9c53-cc47960dcc57)


This JSON configuration defines a workflow that retrieves balance data over TCP/IP, processes it, and sends the appropriate flow speed to a multi-column chromatography device via OPC UA. If the balance value is 55 or lower, the flow speed is set to 2. If the value is 80 or higher, the flow speed is set to 3. For values between 56 and 79, the flow speed is set to 1. The threshold values are exemplary, and IP addresses need to be adjusted according to the specific setup

```json
[
    {
        "id": "3ac596d43f0b4eb3",
        "type": "tcp request",
        "z": "ee5efd3a94c49ad5",
        "name": "",
        "server": "10.226.54.108",
        "port": "55555",
        "out": "time",
        "splitc": "0",
        "x": 630,
        "y": 160,
        "wires": [
            [
                "3a22e9800b9db62a"
            ]
        ]
    },
    {
        "id": "3a22e9800b9db62a",
        "type": "function",
        "z": "ee5efd3a94c49ad5",
        "name": "Process TCP Data",
        "func": "msg.payload = msg.payload.toString().trim();\n\n// Split by space and take the first valid number\nlet parts = msg.payload.split(\" \");\nlet mass = parseFloat(parts[0]);\n\n// Check if it's a valid number\nif (isNaN(mass)) {\n    return null; // Halt flow if not a number\n}\n\nmsg.payload = mass;\nreturn msg;",
        "outputs": 1,
        "timeout": "",
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 860,
        "y": 160,
        "wires": [
            [
                "d9d15ae7e39ab16f"
            ]
        ]
    },
    {
        "id": "d9d15ae7e39ab16f",
        "type": "function",
        "z": "ee5efd3a94c49ad5",
        "name": "Measurement processing & Flow output",
        "func": "msg = processMessage(msg);\nreturn msg;\n\nfunction processMessage(msg) {\n    const payload = Number(msg.payload);\n\n    if (payload <= 55) {\n        msg.payload = 2;\n    } else if (payload >= 80) {\n        msg.payload = 3;\n    } else {\n        msg.payload = 1;\n    }\n\n    return msg;\n}",
        "outputs": 1,
        "timeout": "",
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 1160,
        "y": 160,
        "wires": [
            [
                "605eb78ec6254276"
            ]
        ]
    },
    {
        "id": "605eb78ec6254276",
        "type": "OpcUa-Item",
        "z": "ee5efd3a94c49ad5",
        "item": "ns=3;s=\"OPC_CMD\".\"SELECTMETHOD\"",
        "datatype": "Int16",
        "value": "",
        "name": "SELECTMETHOD",
        "x": 670,
        "y": 280,
        "wires": [
            [
                "cfbf39e397bf1c16"
            ]
        ]
    },
    {
        "id": "cfbf39e397bf1c16",
        "type": "OpcUa-Client",
        "z": "ee5efd3a94c49ad5",
        "endpoint": "5a35a0339f86407a",
        "action": "write",
        "deadbandtype": "a",
        "deadbandvalue": 1,
        "time": 10,
        "timeUnit": "s",
        "certificate": "n",
        "localfile": "",
        "localkeyfile": "",
        "useTransport": false,
        "maxChunkCount": "",
        "maxMessageSize": "",
        "receiveBufferSize": "",
        "sendBufferSize": "",
        "name": "BioSMB WRITE",
        "x": 880,
        "y": 280,
        "wires": [
            [
                "93562acd3a73b685"
            ],
            []
        ]
    },
    {
        "id": "93562acd3a73b685",
        "type": "debug",
        "z": "ee5efd3a94c49ad5",
        "name": "BioSMB READ debug",
        "active": true,
        "tosidebar": true,
        "console": false,
        "tostatus": false,
        "complete": "payload",
        "targetType": "msg",
        "statusVal": "",
        "statusType": "auto",
        "x": 1100,
        "y": 280,
        "wires": []
    },
    {
        "id": "ecb0204dfecc468b",
        "type": "comment",
        "z": "ee5efd3a94c49ad5",
        "name": "",
        "info": "Function node that processes balance payload",
        "x": 820,
        "y": 100,
        "wires": []
    },
    {
        "id": "7b1ef21f28bb5155",
        "type": "comment",
        "z": "ee5efd3a94c49ad5",
        "name": "",
        "info": "Function node that processes incoming mass and gives output based on it",
        "x": 1060,
        "y": 100,
        "wires": []
    },
    {
        "id": "e4d636afc91779b9",
        "type": "comment",
        "z": "ee5efd3a94c49ad5",
        "name": "",
        "info": "OPC UA Write nodes that write the flow output to the equipment",
        "x": 860,
        "y": 340,
        "wires": []
    },
    {
        "id": "5a35a0339f86407a",
        "type": "OpcUa-Endpoint",
        "endpoint": "opc.tcp://10.226.54.118:4840",
        "secpol": "None",
        "secmode": "None",
        "login": false
    }
]
```

## 4. Setup up of a Digital Equipment Representation <br>
![image](https://github.com/user-attachments/assets/885e736f-1c93-4a1a-a487-9bc3ef33cd30)

The following JSON configuration is for setting up a Digital Representation OPC UA server in Node-RED (use example BioSMB_DigitalRepresentation.xml for testing; nneds to be stored in the nodeset directory).

```json
[
    {
        "id": "bf0bd88fcc282f5e",
        "type": "OpcUa-Server",
        "z": "11c6928fc2121e12",
        "port": "53889",
        "name": "",
        "endpoint": "",
        "users": "users.json",
        "nodesetDir": "/home/pi/.node-red/",
        "autoAcceptUnknownCertificate": true,
        "registerToDiscovery": false,
        "constructDefaultAddressSpace": true,
        "allowAnonymous": true,
        "endpointNone": true,
        "endpointSign": true,
        "endpointSignEncrypt": true,
        "endpointBasic128Rsa15": true,
        "endpointBasic256": true,
        "endpointBasic256Sha256": true,
        "maxNodesPerBrowse": 0,
        "maxNodesPerHistoryReadData": 0,
        "maxNodesPerHistoryReadEvents": 0,
        "maxNodesPerHistoryUpdateData": 0,
        "maxNodesPerRead": 0,
        "maxNodesPerWrite": 0,
        "maxNodesPerMethodCall": 0,
        "maxNodesPerRegisterNodes": 0,
        "maxNodesPerNodeManagement": 0,
        "maxMonitoredItemsPerCall": 0,
        "maxNodesPerHistoryUpdateEvents": 0,
        "maxNodesPerTranslateBrowsePathsToNodeIds": 0,
        "maxConnectionsPerEndpoint": 20,
        "maxMessageSize": 4096,
        "maxBufferSize": 4096,
        "maxSessions": 20,
        "x": 460,
        "y": 220,
        "wires": [
            []
        ]
    }
]
```
