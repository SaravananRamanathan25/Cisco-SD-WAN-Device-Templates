# Cisco SD-WAN - Device Templates (REST API)
The Cisco SD-WAN Solution (a.k.a Viptela) is a cloud-delivered overlay SD-WAN architecture that facilitates digital and cloud transformation for enterprises and communication service providers (CSP). It significantly reduces WAN costs and time to deploy new services.

Cisco SD-WAN builds a API based architecture that's crucial for enterprises and CSPs to do the configuration automation through their internal tools.

Once below templates are successfully created,  these can be grouped under one device template which can then attached to an edge device

* Feature Templates
* Local Policy Template
* Security Policy Template

# Device Template - POSTMAN Collection
This postman collection provides some example of various APIs dealing with Device Templates.

This POSTMAN environment and collection that can be used to interact with the Cisco SD-WAN powered by Viptela vManage REST API. You can edit the variables in the environment to point to your own vManage instance. The collection contains REST API calls to create device template, attach device with device template and attach device template with device variable values. Please note that the username should have write permission for "Template Configuration" Feature for the usergroup that it is associated with.

# Steps to execute APIs in the Postman Collection
* Clone or Download the JSON files "CiscoSD-WAN-DeviceTemplate.postman_collection.json" and "Cisco-SD-WAN-Environment.postman_environment.json"  
* Import above files to the POSTMAN  
* In the POSTMAN, make sure you set the environment as "Cisco-SD-WAN-Environment" in the top right corner![SelectEnvDetails](https://github.com/SaravananRamanathan25/Cisco-SD-WAN-Device-Templates/blob/master/Images/SelectEnvDetails-Postman.png)
* Go to Environment options and edit the vmanage, j_username, j_password and port details as per your own vmanage environment![EditEnvDetails](https://github.com/SaravananRamanathan25/Cisco-SD-WAN-Device-Templates/blob/master/Images/UpdateEnvDetails_Postman.png)
* First execute the API under "DeviceTemplate\1.To Get Template ID of Feature Templates\To Get Template ID of Feature Templates".
  * In the response payload, search templateName and find its templateId![SearchFeatureTemplateId](https://github.com/SaravananRamanathan25/Cisco-SD-WAN-Device-Templates/blob/master/Images/SearchFeatureTemplateId.png). For instance, TestTemplate-AAA and TestTemplate-System are the template names you would have created as per our Feature Templates repository [CiscoSD-WAN-FeatureTemplates](https://github.com/SaravananRamanathan25/Cisco-SD-WAN-Feature-Templates)
* Next execute the API under "DeviceTemplate\2.To Get Id of the device\To Get Id of the device.
  * In the response payload, search deviceId or hostname or systemIp and find its deviceType and uuid![SearchDeviceDetails](https://github.com/SaravananRamanathan25/Cisco-SD-WAN-Device-Templates/blob/master/Images/SearchDeviceDetails.png)
* In order to execute the third API under "DeviceTemplate\3.To Create Device Template With Feature Template Attached\To Create Device Template With Feature Template Attached", replace value for below parameters in the request body 
  * deviceType : deviceType fetched from the second API
  * aaa-Feature-TemplateId : templateId of AAA feature template
  * system-vedge-Feature-TemplateId : templateId of System feature template
  * After replacing the values, payload will somewhat look like as shown in screenshot![SampleCreateDeviceTemplatePayload](https://github.com/SaravananRamanathan25/Cisco-SD-WAN-Device-Templates/blob/master/Images/SampleCreateDeviceTemplatePayload.png) 
* Next execute the API under "DeviceTemplate\4.To Get Template ID of Device Template\To Get Template ID of Device Template".
  * In the response payload, search templateName and find its templateId![SearchDeviceTemplateId](https://github.com/SaravananRamanathan25/Cisco-SD-WAN-Device-Templates/blob/master/Images/SearchDeviceTemplateId.png). For instance, Test-DeviceTemplate is the template name you would have created using  third API	
* In order to execute the fifth API under "DeviceTemplate\5.To Attach Device With Device Template\To Attach Device With Device Template", replace value for below parameters in the request body 
  * Device-TemplateId : templateId fetched from the fourth API
  * deviceIds : uuid fetched from the second API
  * On successful execution of above api, vManage will return the device input variables as shown here![SampleAttachDevicewithDeviceTemplateOutput](https://github.com/SaravananRamanathan25/Cisco-SD-WAN-Device-Templates/blob/master/Images/SampleAttachDevicewithDeviceTemplateOutput.png). 
Copy the output payload to a notepad.	
* In order to execute the final API under "DeviceTemplate\6.To Attach Device Template With Device Variable Values\To Attach Device Template With Device Variable Values", 
  * In the request body replace Device-TemplateId with templateId fetched from the fourth API
  * From the notepad (which you have copy pasted in the above step), cut all the data present inside the "data" array and paste the same in the request payload. Enter value for all the variables as per your requirement.
  * After replacing the values, payload will somewhat look like as shown in screenshot![SampleAttachDeviceTemplatewithDeviceVariableValuesPayload](https://github.com/SaravananRamanathan25/Cisco-SD-WAN-Device-Templates/blob/master/Images/SampleAttachDeviceTemplatewithDeviceVariableValuesPayload.png)
* We have successfully created a device template and attached to a device.
