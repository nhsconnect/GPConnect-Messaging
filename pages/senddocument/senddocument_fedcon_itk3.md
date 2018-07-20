---
title: Send Federated Consultation Summary - ITK3 Header
keywords: itk3
tags: [itk3]
sidebar: senddocument_sidebar
permalink: senddocument_fedcon_itk3.html
summary: "Details of how the ITK3 header is populated to fulfil the Send Federated Consultation use case"
---

Please refer to [Using ITK3 to support GP Connect Messaging](integration_itk3.html) for an overview of the use of ITK3 in this context.

The following specific requirements describe how the [ITK3 Message Header](https://fhir.nhs.uk/STU3/StructureDefinition/ITK-MessageHeader-2) MUST be populated in all instances of messages generated by federated practices for this use case:


| Message Header Item |	Description |
| ------------------- | ------------ |
| RecipientType | Fixed value: *FA* (“For action”) taken from ValueSet [https://fhir.nhs.uk/STU3/CodeSystem/ITK-RecipientType-1](https://fhir.nhs.uk/STU3/CodeSystem/ITK-RecipientType-1) <br/>  <br/>  The meaning of `RecipientType` is applied in a common way across all ITK3 messaging.  “For action” in this case indicates that the recipient is expected to take the action of attaching the payload contents to the patient record. (“For information” is analogous to an email “CC” where no action is expected from the recipient, and the message could be deleted.) <br/>  <br/>  This item is found in the ITKMessageHandling extension within the [ITK3 Message Header](https://fhir.nhs.uk/STU3/StructureDefinition/ITK-MessageHeader-2). |
|Priority |	Fixed value: *routine* taken from https://fhir.nhs.uk/STU3/ValueSet/ITK-Priority-1 <br/>  <br/>  Where specific action beyond attachment to patient record is expected, existing business processes should be used as the “write-back” is simply the act of synchonising with the registered patient record. Alternatively, when the GP Connect “Send Task” capability has been implemented, this could be used. <br/>  <br/>  This item is found in the ITKMessageHandling extension within the [ITK3 Message Header](https://fhir.nhs.uk/STU3/StructureDefinition/ITK-MessageHeader-2). |
| BusAckRequested |	Fixed value: *true* which will request a ITK3 Response with a response code in the range 30001 to 30003. <br/>  <br/>  This item is found in the ITKMessageHandling extension within the[ITK3 Message Header](https://fhir.nhs.uk/STU3/StructureDefinition/ITK-MessageHeader-2). |
| InfAckRequested |Fixed value : *true* which will request a ITK3 Response with a response code in the range 10001 to 20013. <br/>  <br/>  This item is found in the ITKMessageHandling extension within the [ITK3 Message Header](https://fhir.nhs.uk/STU3/StructureDefinition/ITK-MessageHeader-2). |
| SenderReference |	Unique identifier of the encounter which has taken place at the federated practice  <br/>  <br/>   This item is found in the ITKMessageHandling extension within the [ITK3 Message Header](https://fhir.nhs.uk/STU3/StructureDefinition/ITK-MessageHeader-2). |
| MessageDefinition | Fixed value of https://fhir.nhs.uk/STU3/MessageDefinition/ITK-SendTask-MessageDefinition-Instance-1 <br/>  <br/> This item is found in the ITKMessageHandling extension within the [ITK3 Message Header](https://fhir.nhs.uk/STU3/StructureDefinition/ITK-MessageHeader-2). |
| Sender | Reference to CareConnect-ITK-Header-Organization-1 resource present in the ITK Header |
| source | MESH mailbox ID of the sender |
| Event | Fixed code value of `ITK007C` from code system https://fhir.nhs.uk/STU3/CodeSystem/ITK-MessageEvent-2 |
| Timestamp	| The date/time when the message was generated. (A separate process such as the MESH client may be responsible for sending the message at a later date/time.) |

The following table indicates those elements which MUST NOT be present in the ITK3 Message Header

| Message Header Item |	Note |
| ------------------- | ------------ |
| destination	| As MESH routing SHALL be used to route message to registered practice by NHS Number, DOB and Surname, this element is not required |
| receiver |  As MESH routing SHALL be used to route message to registered practice by NHS Number, DOB and Surname, this element is not required |

 
## ITK3 Responses Generated ##

The following specific requirements describe how the [ITK3 Message Header](https://fhir.nhs.uk/STU3/StructureDefinition/ITK-MessageHeader-2) MUST be populated in all instance of messages generated by the registered practice as an ITK Response:

| Message Header Item |	Description |
| ------------------- | ------------ |
| BusAckRequested |	Fixed value: *false* <br/>  <br/>  This item is found in the ITKMessageHandling extension within the[ITK3 Message Header](https://fhir.nhs.uk/STU3/StructureDefinition/ITK-MessageHeader-2). |
| InfAckRequested |Fixed value : *false* <br/>  <br/>  This item is found in the ITKMessageHandling extension within the [ITK3 Message Header](https://fhir.nhs.uk/STU3/StructureDefinition/ITK-MessageHeader-2). |
| SenderReference |	Unique identifier of the encounter which has taken place at the federated practice  <br/>  <br/>   This item is found in the ITKMessageHandling extension within the [ITK3 Message Header](https://fhir.nhs.uk/STU3/StructureDefinition/ITK-MessageHeader-2). |
| Sender | Reference to CareConnect-ITK-Header-Organization-1 resource present in the ITK Header |
| Event | Fixed code value of `ITK008M` from code system https://fhir.nhs.uk/STU3/CodeSystem/ITK-MessageEvent-2 |
| Timestamp	| The date/time when the message was generated. (A separate process such as the MESH client may be responsible for sending the message at a later date/time.) |