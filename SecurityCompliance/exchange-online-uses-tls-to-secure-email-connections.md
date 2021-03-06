---
title: "How Exchange Online uses TLS to secure email connections in Office 365"
ms.author: krowley
author: kccross
manager: laurawi
ms.date: 10/11/2017
ms.audience: ITPro
ms.topic: reference
ms.service: o365-administration
localization_priority: Normal
ms.collection: Strat_O365_IP
search.appverid:
- MET150
- MOE150
ms.assetid: 4cde0cda-3430-4dc0-b489-f2c0736c929f
description: "Learn how Exchange Online and Office 365 use Transport Layer Security (TLS) and Forward Secrecy (FS) to secure email communications. Also get information about the certificate issued by Microsoft for Exchange Online."
---

# How Exchange Online uses TLS to secure email connections in Office 365

Learn how Exchange Online and Office 365 use Transport Layer Security (TLS) and Forward Secrecy (FS) to secure email communications. Also provides information about the certificate issued by Microsoft for Exchange Online.
  
## TLS basics for Office 365 and Exchange Online

Transport Layer Security (TLS), and SSL that came before TLS, are cryptographic protocols that secure communication over a network by using security certificates to encrypt a connection between computers. TLS supersedes Secure Sockets Layer (SSL) and is often referred to as SSL 3.1. For Exchange Online, we use TLS to encrypt the connections between our Exchange servers and the connections between our Exchange servers and other servers such as your on-premises Exchange servers or your recipients' mail servers. Once the connection is encrypted, all data sent through that connection is sent through the encrypted channel. However, if you forward a message that was sent through a TLS-encrypted connection, that message isn't necessarily encrypted. This is because, in simple terms, TLS doesn't encrypt the message, just the connection.
  
If you want to encrypt the message you need to use an encryption technology that encrypts the message contents, for example, something like Office Message Encryption. See [Email encryption in Office 365](email-encryption.md) and [Office 365 Message Encryption (OME)](ome.md) for information on message encryption options in Office 365. 
  
We recommend using TLS in situations where you want to set up a secure channel of correspondence between Office 365 and your on-premises organization or another organization, such as a partner. Exchange Online always attempts to use TLS first to secure your email but cannot always do this if the other party does not offer TLS security. Keep reading to find out how you can secure all mail to your on-premises servers or important partners by using  *connectors*  . 
  
## How Exchange Online uses TLS between Exchange Online customers

Exchange Online servers always encrypt connections to other Exchange Online servers in our datacenters with TLS 1.2. When you send mail to a recipient that is within your Office 365 organization, that email is automatically sent over a connection that is encrypted using TLS. Also, all email that you send to other Office 365 customers is sent over connections that are encrypted using TLS and are secured using Forward Secrecy.
  
## How Office 365 uses TLS between Office 365 and external, trusted partners

By default, Exchange Online always uses opportunistic TLS. This means Exchange Online always tries to encrypt connections with the most secure version of TLS first, then works its way down the list of TLS ciphers until it finds one on which both parties can agree. Unless you have configured Exchange Online to ensure that messages to that recipient are only sent through secure connections, then by default the message will be sent unencrypted if the recipient organization doesn't support TLS encryption. Opportunistic TLS is sufficient for most businesses. However, for business that have compliance requirements such as medical, banking, or government organizations, you can configure Exchange Online to require, or force, TLS. For instructions, see [Configure mail flow using connectors in Office 365](https://technet.microsoft.com/library/ms.exch.eac.connectorselection%28v=exchg.150%29.aspx).
  
If you decide to configure TLS between your organization and a trusted partner organization, Exchange Online can use forced TLS to create trusted channels of communication. Forced TLS requires your partner organization to authenticate to Exchange Online with a security certificate in order to send mail to you. Your partner will need to manage their own certificates in order to do this. In Exchange Online, we use connectors to protect messages that you send from unauthorized access before they arrive at the recipient's email provider. For information on using connectors to configure mail flow, see [Configure mail flow using connectors in Office 365](https://technet.microsoft.com/library/ms.exch.eac.connectorselection%28v=exchg.150%29.aspx).
  
## TLS and hybrid Exchange Server deployments

If you are managing a hybrid Exchange deployment, your on-premises Exchange server needs to authenticate to Office 365 using a security certificate in order to send mail to recipients whose mailboxes are only in Office 365. As a result, you need to manage your own security certificates for your on-premises Exchange servers. You must also securely store and maintain these server certificates. For more information about managing certificates in hybrid deployments, see [Certificate requirements for hybrid deployments](https://technet.microsoft.com/library/hh563848%28v=exchg.150%29.aspx).
  
## How to set up forced TLS for Exchange Online in Office 365

For Exchange Online customers, in order for forced TLS to work to secure all of your sent and received email, you need to set up more than one connector that requires TLS. You'll need one connector for email sent to your user mailboxes and another connector for email sent from your user mailboxes. Create these connectors in the Exchange admin center in Office 365. For instructions, see [Configure mail flow using connectors in Office 365](https://technet.microsoft.com/library/ms.exch.eac.connectorselection%28v=exchg.150%29.aspx).
  
## TLS certificate information for Exchange Online

The certificate information used by Exchange Online is described in the following table. If your business partner is setting up forced TLS on their email server, you will need to provide this information to them. Be aware that for security reasons, our certificates do change from time to time. Currently, we are rolling out an update to our certificate within our datacenters. The new certificate is valid from April 15, 2016.
  
 **Current certificate information valid from April 15, 2016**
  
|**Attribute**|**Value**|
|:-----|:-----|
|Certificate authority root issuer  <br/> |Baltimore CyberTrust Root  <br/> |
|Certificate name  <br/> |mail.protection.outlook.com  <br/> |
|Organization  <br/> |Microsoft Corporation  <br/> |
|Organization unit  <br/> |Microsoft Corporation  <br/> |
|Certificate key strength  <br/> |2048  <br/> |
   
 **Deprecated certificate information valid until May 15, 2016**
  
To help ensure a smooth transition, we will continue to provide the old certificate information for your reference for some time, however, you should use the current certificate information from now on.
  
****

|**Attribute**|**Value**|
|:-----|:-----|
|Certificate authority root issuer  <br/> |Baltimore CyberTrust Root  <br/> |
|Certificate name  <br/> |mail.protection.outlook.com  <br/> |
|Organization  <br/> |Microsoft  <br/> |
|Organization unit  <br/> |Forefront Online Protection for Exchange  <br/> |
|Certificate key strength  <br/> |2048  <br/> |
   
## Get more information about TLS and Office 365

For a list of supported cipher suites, see [Technical reference details about encryption in Office 365](technical-reference-details-about-encryption.md).
  
[Set up connectors for secure mail flow with a partner organization](https://technet.microsoft.com/library/dn751021%28v=exchg.150%29.aspx)
  
[Connectors with enhanced email security](https://technet.microsoft.com/library/261d92e4-7371-4555-b781-2062b5bb5278.aspx)
  
[Encryption in Office 365](encryption.md)
  

