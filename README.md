# Cisco SD-WAN - DeviceTemplate (REST API)
The Cisco SD-WAN Solution (a.k.a Viptela) is a cloud-delivered overlay SD-WAN architecture that facilitates digital and cloud transformation for enterprises and communication service providers (CSP). It significantly reduces WAN costs and time to deploy new services.

Cisco SD-WAN builds a API based architecture that's crucial for enterprises and CSPs to do the configuration automation through their internal tools.

Once below templates are successfully created,  these can be grouped under one device template which can then attached to an edge device

Feature Templates
Local Policy Template
Security Policy Template

# Device Template - POSTMAN Collection

This postman collection provides some example of various APIs dealing with Device Templates.

This POSTMAN environment and collection that can be used to interact with the Cisco SD-WAN powered by Viptela vManage REST API. You can edit the variables in the environment to point to your own vManage instance. The collection contains REST API calls to create device template, attach device with device template and attach device template with device variable values. Please note that the username should have write permission for "Template Configuration" Feature for the usergroup that it is associated with.

# Steps to execute APIs in the Postman Collection
* Clone or Download the JSON files "CiscoSD-WAN-DeviceTemplate.postman_collection.json" and "Cisco-SD-WAN-Environment.postman_environment.json"  
* Import above files to the POSTMAN  
* In the POSTMAN, make sure you set the environment as "Cisco-SD-WAN-Environment" in the top right corner  
* Go to Environment options and edit the vmanage, j_username, j_password and port details as per your own vmanage environment
* In order to execute the first API under "DeviceTemplate\1.To Create Device Template With Feature Template Attached\To Create Device Template With Feature Template Attached", replace value for below parameters in the request body 
	* deviceType : type of the device 
	* aaa-Feature-TemplateId : templateId returned by vManage on successful execution of "To Create AAA Feature Template"
	* system-vedge-Feature-TemplateId : templateId returned by vManage on successful execution of "To Create System Feature Template"
	
		After replacing the values, payload will somewhat look like as,
		{
			"templateName": "Test-DeviceTemplate",
			"templateDescription": "Test-DeviceTemplate",
			"deviceType": "vedge-100-B",
			"configType": "template",
			"factoryDefault": false,
			"policyId": "",
			"featureTemplateUidRange": [],
			"connectionPreferenceRequired": true,
			"connectionPreference": true,
			"generalTemplates": [{
				"templateId": "ca0653cd-22d8-414c-a904-ea701ed4a465",
				"templateType": "aaa"
			},
			{
				"templateId": "a1d6e518-f105-401e-a099-f08dd091174f",
				"templateType": "system-vedge"
			}
			]
		}
	On successful execution of above api, vManage will return the device templateId
	
* In order to execute the second API under "DeviceTemplate\2.To Attach Device With Device Template\To Attach Device With Device Template", replace value for below parameters in the request body 
	* Device-TemplateId : templateId returned by vManage on successful execution of the first API "To Create Device Template With Feature Template Attached" 
	* deviceIds : uuid of the device. This value can be fetched using an api https://{{vmanage}}:{{port}}/dataservice/device

		After replacing the values, payload will somewhat look like as,
		{
			"templateId": "f5e90ae4-57aa-430d-b273-f12576275f1c",
			"deviceIds": ["11OG435170388"],
			"isEdited": false,
			"isMasterEdited": false
		}
	On successful execution of above api, vManage will return the device input variables. Copy the output payload to a notepad.
	
	• In order to execute the final API under "DeviceTemplate\3.To Attach Device Template With Device Variable Values\To Attach Device Template With Device Variable Values", 
		○ In the request body replace Device-TemplateId with templateId returned by vManage on successful execution of the first API "To Create Device Template With Feature Template Attached"
		○ From the notepad (which you have copy pasted in the above step), cut all the data present inside the "data" array and paste the same in the request payload. Enter value for all the variables as per your requirement.
		After replacing the values, payload will somewhat look like as,
		{
			"templateId": "f5e90ae4-57aa-430d-b273-f12576275f1c",
			"device": {
				"csv-status": "complete",
				"csv-deviceId": "11OG435170388",
				"csv-deviceIP": "10.44.250.17",
				"csv-host-name": "Exeter-1",
				"//system/host-name": "Exeter-1",
				"//system/system-ip": "10.44.250.17",
				"//system/site-id": 60,
				"/0/vpn_if_name_Default_vEdge_DHCP_Tunnel_Interface/interface/if-name": "ge0/4",
				"//system/aaa/auth-order": ["local",
				"radius",
				"tacacs"],
				"//system/aaa/auth-fallback": true,
				"//system/aaa/admin-auth-order": true,
				"//system/aaa/logs/netconf-disable": true,
				"csv-templateId": "f5e90ae4-57aa-430d-b273-f12576275f1c",
				"vipEnumListClone_//system/aaa/auth-order": ["local",
				"radius",
				"tacacs"]
			},
			"isRFSRequired": true,
			"isEdited": false,
			"isMasterEdited": false
		}
		
	
