# Low-Code-Repository
Repository of Node-RED Low-Code Use Cases

1. Online model deployment and integration into a SCADA system
2. Data Dashboarding and Monitoring
3. Interfacing of Equipment and Flow Control Automation for Multi-Column Chromatography Systems
5. Setup up of a Digital Equipment Representation <br>
![image](https://github.com/user-attachments/assets/0c8b4323-4efa-448c-aaf6-21c6a515c137)

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
