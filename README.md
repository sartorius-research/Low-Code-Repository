# Low-Code-Repository
Repository of Node-RED Low-Code Use Cases

1. Online model deployment and integration into a SCADA system <br>
![image](https://github.com/user-attachments/assets/f78c080b-c8b3-46e8-8736-c357b818c030)

This JSON configuration defines an workflow that is retrieving spectroscopy data, puts it into a model and feeds the model outcome into and OPC UA server that can be accessed by a SCADA system.

```json
[
    {
        "id": "86ce3655a71bd54a",
        "type": "OpcUa-Item",
        "z": "b3712e4a33f45cb9",
        "item": "ns=5;s=\\\\.\\Futura 02\\Zeroed Averaged Capacitance Values",
        "datatype": "Float Array",
        "value": "",
        "name": "Zeroed Averaged Capacitance values",
        "x": 770,
        "y": 360,
        "wires": [
            [
                "a5e9c11330d3b998"
            ]
        ]
    },
    {
        "id": "ecb42cf9b37451bf",
        "type": "OpcUa-Item",
        "z": "b3712e4a33f45cb9",
        "item": "ns=1;s=viamass-VCC",
        "datatype": "Double",
        "value": "",
        "name": "viamass-VCC",
        "x": 1650,
        "y": 360,
        "wires": [
            [
                "a65d9f5dd6f30b03"
            ]
        ]
    },
    {
        "id": "a65d9f5dd6f30b03",
        "type": "OpcUa-Client",
        "z": "b3712e4a33f45cb9",
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
        "useTransport": false,
        "maxChunkCount": 1,
        "maxMessageSize": 8192,
        "receiveBufferSize": 8192,
        "sendBufferSize": 8192,
        "name": "",
        "x": 1840,
        "y": 360,
        "wires": [
            [],
            []
        ]
    },
    {
        "id": "fdbdf326d02dae13",
        "type": "function",
        "z": "b3712e4a33f45cb9",
        "name": "Spectroscopy Model",
        "func": "msg.payload = -1.11411+msg.payload[0]*-0.0846305+msg.payload[1]*-0.0693173+msg.payload[2]*-0.0509203+msg.payload[3]*-0.0266838+msg.payload[4]*-0.00368787+msg.payload[5]*0.0244135+msg.payload[6]*0.0543474+msg.payload[7]*0.0815575+msg.payload[8]*0.100042+msg.payload[9]*0.109601+msg.payload[10]*0.107292+msg.payload[11]*0.0949137+msg.payload[12]*0.0787177+msg.payload[13]*0.0704221+msg.payload[14]*0.0454615+msg.payload[15]*0.0338642+msg.payload[16]*0.0239638+msg.payload[17]*0.0169988+msg.payload[18]*0.0131833+msg.payload[19]*0.00917408+msg.payload[20]*0.00747873+msg.payload[21]*0.00519937+msg.payload[22]*0.00307098+msg.payload[23]*0.00225113+msg.payload[24]*0.00143756\nreturn msg;",
        "outputs": 1,
        "timeout": "",
        "noerr": 0,
        "initialize": "",
        "finalize": "",
        "libs": [],
        "x": 1400,
        "y": 360,
        "wires": [
            [
                "ecb42cf9b37451bf"
            ]
        ]
    },
    {
        "id": "4bb1da24c6e28510",
        "type": "inject",
        "z": "b3712e4a33f45cb9",
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
        "x": 760,
        "y": 540,
        "wires": [
            [
                "49e1b80836fc1f7d"
            ]
        ]
    },
    {
        "id": "49e1b80836fc1f7d",
        "type": "OpcUa-Server",
        "z": "b3712e4a33f45cb9",
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
        "maxSessions": 20,
        "x": 1040,
        "y": 540,
        "wires": [
            []
        ]
    },
    {
        "id": "f93a2e6e9baa3255",
        "type": "comment",
        "z": "b3712e4a33f45cb9",
        "name": "",
        "info": "Receiving Spectroscopy Raw Data from OPC UA Server",
        "x": 680,
        "y": 300,
        "wires": []
    },
    {
        "id": "05e83eef11cdf9dc",
        "type": "comment",
        "z": "b3712e4a33f45cb9",
        "name": "",
        "info": "OPC UA Server that is initiated to offer the outcome of the model",
        "x": 680,
        "y": 480,
        "wires": []
    },
    {
        "id": "67cd2dd521a49f6e",
        "type": "comment",
        "z": "b3712e4a33f45cb9",
        "name": "",
        "info": "OPC UA Node ID that is receiving the model outcome and can be accessed by SCADA system.",
        "x": 1620,
        "y": 300,
        "wires": []
    },
    {
        "id": "a5e9c11330d3b998",
        "type": "OpcUa-Client",
        "z": "b3712e4a33f45cb9",
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
        "useTransport": false,
        "maxChunkCount": 1,
        "maxMessageSize": 8192,
        "receiveBufferSize": 8192,
        "sendBufferSize": 8192,
        "name": "OPC UA Client for Viamass",
        "x": 1100,
        "y": 360,
        "wires": [
            [
                "fdbdf326d02dae13"
            ],
            []
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
    }
]
```

3. Data Dashboarding and Monitoring <br>

```json

```
5. Interfacing of Equipment and Flow Control Automation for Multi-Column Chromatography Systems <br>

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

7. Setup up of a Digital Equipment Representation <br>
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
