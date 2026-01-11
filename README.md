# 🤖 AzureQnABot

This project delivers a **secure, serverless Question-and-Answer (QnA) bot** integrated with **Microsoft Teams**, built using **Azure Language Services**, **Azure AI Search**, and other core Azure components. The bot enables natural, conversational interactions over Microsoft Teams to retrieve answers from enterprise documents.

---

## 📌 Project Description

This project involves the development and deployment of a **Microsoft Teams-integrated QnA Bot** using **Azure Language Services** and **Azure AI Search**, tailored specifically to enhance document-based knowledge retrieval. Leveraging the advanced **natural language processing** and **semantic search** capabilities of Azure AI, this bot is strategically designed to:

- Improve **information accessibility**
- Promote **standardization** with customizable knowledge base
- Enhance **time efficiency** in finding accurate answers
- Maintain **compliance** with organizational policies

The bot enables users to interact with enterprise documents conversationally, mining answers directly from uploaded resources like PDFs, DOCX, and TXT files. It is hosted in a **fully secure infrastructure**, using:

- **Azure Private Endpoints** to eliminate public exposure of backend services  
- **Azure Application Gateway** with WAF to securely expose the bot on the public internet without directly exposing backend components  
- **Azure Virtual Network** to encapsulate all resources under a private, controlled environment  

This initiative empowers users to access reliable, governed knowledge through a friendly Teams chat interface, supporting scalable, secure, and intelligent enterprise interactions.

---

## 🚀 Built With

- **Azure Language Services (QnA)**
- **Azure AI Search**
- **Azure Blob Storage**
- **Azure Application Gateway**
- **Azure Private Endpoints**
- **Microsoft Teams**

---

## 🔐 Project Goals

- Fully secure deployment — **no public access** to backend services  
- Private access via **Application Gateway** + **Private Endpoints**  
- Integrated with **Microsoft Teams** for a natural Q&A experience  
- Uses **Azure Cognitive Services** for language understanding and document-based knowledge mining  

---

## ⚙️ Architecture Overview

```
[Microsoft Teams] 
     ↓
[Azure Bot Framework] 
     ↓
[Azure Application Gateway (WAF Enabled)]
     ↓
[Private Endpoint]
     ↓
[Azure App Service / Azure Function App]
   ├──> [Azure Language Service (QnA)]
   └──> [Azure AI Search]
```

---

## 🔧 Azure Services Used

| Azure Service              | Purpose                                                                 |
|---------------------------|-------------------------------------------------------------------------|
| **Azure AI Language**     | Provides QnA Maker-style language understanding                        |
| **Azure AI Search**       | Indexes documents from `qna-docs/` for semantic search                 |
| **Azure Blob Storage**    | Stores uploaded `.pdf`, `.docx`, `.txt` documents                      |
| **Azure Web App Bot**     | Hosts and manages the Teams-integrated bot                             |
| **Azure Private Endpoints** | Locks down access to only private networks                            |
| **Azure Virtual Network** | Provides a secure environment for all components                      |
| **Azure Application Gateway** | Provides TLS termination and secure public routing with WAF         |
| **Microsoft Teams**       | Final interface where users interact with the QnA bot                  |

---

## ✅ Step-by-Step Deployment Guide

### 1. Create Resource Group & Virtual Network

- **Resource Group**: `QnABotRG`
- **Virtual Network**: `QnABotVNet`
  - Subnets:
    - `PrivateEndpointSubnet`
    - `AppGatewaySubnet`
    - `BotSubnet` *(optional)*

---

### 2. Set Up Azure Blob Storage

- **Container Name**: `qna-docs`
- Upload documents (`.pdf`, `.docx`, `.txt`) to act as your knowledge base.

---

### 3. Create Azure AI Search Service

- Create a **Search Service**
- Define an **index** using the Blob Storage container
- Load and test the indexed data

---

### 4. Create Azure AI Language Resource (Language Studio)

- **Resource Name**: `QNA-BOT-LANG-05`
- Author a QnA project
- Connect it to the AI Search index
- Publish the project for use in the bot

---

### 5. Register the Bot (Azure Bot Channels)

- Register your bot under Azure Bot Services
- Enable **Microsoft Teams** as a channel
- Save:
  - **Microsoft App ID**
  - **Client Secret**

---

### 6. Create Private Endpoint

- **Target Service**: `QNA-BOT-LANG-05`
- **Subnet**: `PrivateEndpointSubnet`
- **Private DNS Zone**: `privatelink.cognitiveservices.azure.com`

---

### 7. Configure Private DNS

- Create a **Private DNS Zone**
- Link to `QnABotVNet`
- Ensure resolution of:  
  `qna-bot-lang-05.privatelink.cognitiveservices.azure.com → Private IP`

---

### 8. Deploy Azure Application Gateway (Optional but Recommended)

- Deploy in `AppGatewaySubnet`
- Configure:
  - TLS/SSL certificates
  - Routing rules to forward requests to bot backend
  - Web Application Firewall (WAF) policies

---

### 9. Test the Bot in Microsoft Teams

- Use **Teams App Studio** or Bot Channels Registration
- Input the **Bot App ID**
- Start chatting and test QnA capabilities

---


## 📌 Notes

- Keep all resources in the same region to avoid private DNS and endpoint conflicts.
- Ensure **NSGs** and **firewall rules** allow communication within the VNet.
- The success of private access depends on correct **DNS zone** linking and endpoint configuration.

---

## 👤 Author

**Sarthak Gupta**  
📧 *sarthakgupta1723@gmail.com*
    *www.linkedin.com/in/sarthak-gupta-cloudengineer*



