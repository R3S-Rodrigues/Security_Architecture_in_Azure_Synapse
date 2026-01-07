# Security_Architecture_in_Azure_Synapse
A arquitetura de segurança do Azure Synapse, abordando conectividade, gerenciamento de endpoints e governança. O objetivo é oferecer uma visão clara sobre a segurança de dados e o acesso controlado. Serve como referência para desenvolvedores e analistas que buscam melhorar suas implementações de segurança no Azure Synapse

# Visão Geral / Overview

Esta arquitetura descreve como implementar uma estrutura segura, auditável e escalável para ambientes de dados usando o Azure Synapse Analytics. Ela garante isolamento de rede, conectividade privada e governança contínua.

# Arquitetura / architecture
![Security architecture in Azure Synapse](https://github.com/user-attachments/assets/d8b4d87e-165f-4088-a88f-e0782911eca4)

# Componentes da Arquitetura / Architecture Components

🔹 Ambiente do Usuário / User Environment

Usuário / Analista acessa via VNet Hub/Spoke

🔹 Ambiente de Conectividade / Connectivity Environment

Private Endpoints:

Web Private Endpoint → IP: 172.16.12.5 → Porta: 443

SQL Private Endpoint → IP: 172.16.12.6 → Porta: 1433

SqlOnDemand Private Endpoint → IP: 172.16.12.7 → Porta: 1433

Azure Private DNS Zones:

privatelink.dev.azuresynapse.net

privatelink.sql.azuresynapse.net

privatelink.ondemand.sql.azuresynapse.net

Subnets dedicadas com NSG por função

🔹 Ambiente Gerenciado Azure / Managed Azure Environment

Synapse Gateway

Dedicated SQL Pool

Serverless SQL Pool

Apache Spark Pools (opcional)

Data Lake Gen2 Storage (via Managed Private Endpoints)

# Segurança e Isolamento / Security and Isolation

Tráfego 100% privado via Private Endpoints

Resolução DNS interna via Azure Private DNS

Portas restritas e controladas (443/1433)

Subnets com NSG e regras de saída bloqueando acesso público

# Governança e Monitoramento / Governance and Monitoring

NSG Flow Logs → Azure Monitor / Log Analytics

Defender for Cloud (recomendado)

Auditoria contínua e rastreabilidade de tráfego

# Checklist de Validação / Validation Checklist

[ ] DNS resolve para IP privado via nslookup <workspace>.sql.azuresynapse.net

[ ] Portas 443 e 1433 acessíveis apenas via VNet

[ ] NSG com regras específicas por subnet

[ ] Logs visíveis no Log Analytics

[ ] Studio, SSMS e Power BI conectam via privatelink

[ ] Managed VNet habilitada no workspace

# Notas Operacionais / Operational Notes

Naming conventions por tipo de recurso

RBAC aplicado por função (analista, engenheiro, auditor)

Tagging para rastreabilidade e automação

VNet Peering para ambientes multi-VNet

# Conclusão / Final Notes

Esta arquitetura oferece uma base sólida para ambientes de dados seguros e auditáveis no Azure Synapse. Ela pode ser usada como referência técnica em entrevistas, publicações ou documentação corporativa.
