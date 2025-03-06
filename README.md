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
        "wires": [["fdacac07a22735e2"]]
    },
    {
        "id": "fdacac07a22735e2",
        "type": "OpcUa-Client",
        "z": "b3712e4a33f45cb9",
        "endpoint": "4f3a5d493bf11d53",
        "action": "read",
        "deadbandtype": "a",
        "deadbandvalue": 1,
        "time": 10,
        "timeUnit": "s",
        "certificate": "n",
        "securitymode": "None",
        "securitypolicy": "None",
        "name": "OPC UA Client for Viamass",
        "x": 1110,
        "y": 360,
        "wires": [["fdbdf326d02dae13"], []]
    }
]
```

3. Data Dashboarding and Monitoring
4. Interfacing of Equipment and Flow Control Automation for Multi-Column Chromatography Systems
5. Setup up of a Digital Equipment Representation <br>
![image](https://github.com/user-attachments/assets/885e736f-1c93-4a1a-a487-9bc3ef33cd30)

The following JSON configuration is for setting up a Digital Representation OPC UA server in Node-RED (use example BioSMB_DigitalRepresentation.xml for testing; nneds to be stored in the nodeset directory).

```json
[
    {
        "id": "bf0bd88fcc282f5e",
        "type": "OpcUa-Server",
        "z": "11c6928fc2121e12",
        "port": "53889",
        "name": "BioSMB Digital Representation",
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
        "x": 1590,
        "y": 340,
        "wires": [[]]
    }
]
```
