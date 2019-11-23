# cda2fhir-service
CDA To Fhir (JSON) Service uses the cda2fhir library by amida-tech to provide a service that accepts a CDA formatted XML 
document and returns the data converted to fhir in JSON format.  It supports FHIR 3.

# Binary Download and Install 

The download allows for install in Tomcat and other tools. This service is a good 
candidate for container services such as AWS Elastic Beanstalk.

Download the WAR directly from the master branch. See `cda2fhir-service-0.0.1.war`.


## Build Instructions Installation

Apache Maven is required to build cda2fhir-service. Please visit http://maven.apache.org/ in order to install Maven on your system.

Under the root directory of the cda2fhir-service project run the following:

	$ cda2fhir-service> mvn install

In order to make a clean install run the following:

	$ cda2fhir-service> mvn clean install
	
To run the server locally:

	$ cda2fhir-service> mvn spring-boot:run

	
## API Overview
The API is RESTFUL and accepts application/xml and returns the fhir results in application/json

### Health Endpoints
##### GET /actuator/health
###### Response
```
{"status":"UP"}
```

##### GET /actuator/info
###### Response TBD
```
{}
```

### REST API Endpoints
  
##### GET /api/convert
```
  {
    "message" : "Welcome to the CDA to FHIR Conversion Service"
  }
```

##### POST /api/convert [consumes application/xml]
###### Sample Request (partial)
```
  <?xml version="1.0" encoding="UTF-8"?>
  <ClinicalDocument xmlns="urn:hl7-org:v3">
      <realmCode code="US"/>
      <typeId root="2.16.840.1.113883.1.3" extension="POCD_HD000040"/>
      ...
      ...
  </ClinicalDocument>
```
###### Sample curl Request
```
curl http://cda2fhirservice/api/convert -X POST -d @cda-filename.xml -H "Content-Type: application/xml"
```

###### Sample Response (partial)
```
  {
    "entry": [
      {
        "resource": {
          "id": "1",
          "subject": {
            "display": "MICKEY M MOUSE, MICKEY MOUSE",
            "reference": "Patient/2"
          },
          "author": [
            {
              "reference": "Device/3"
            }
          ],
          "resourceType": "Composition",
          ...
          ...
        }
      }
    ]
  }  
```




