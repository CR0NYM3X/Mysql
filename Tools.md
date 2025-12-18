 

### ✅ **Soluciones Nativas de MySQL**

1.  **MySQL Replication (Asíncrona/Semi-Síncrona)**
    *   **Tipo:** Open Source (incluido en MySQL Community)
    *   **Función:** Replica datos entre servidores para alta disponibilidad y recuperación ante desastres.
    *   **Notas:** No garantiza consistencia total en semi-síncrona, pero es muy usada.

2.  **MySQL Group Replication**
    *   **Tipo:** Open Source (MySQL Community)
    *   **Función:** Alta disponibilidad con replicación multi-master y tolerancia a fallos.
    *   **Notas:** Base para **InnoDB Cluster**.

3.  **MySQL InnoDB Cluster**
    *   **Tipo:** Open Source (requiere MySQL Shell)
    *   **Función:** Solución completa para HA con failover automático.
    *   **Notas:** Ideal para entornos críticos.

4.  **MySQL Router**
    *   **Tipo:** Open Source
    *   **Función:** Balanceo de carga y redirección automática en clusters.

***

### ✅ **Herramientas Open Source Externas**

5.  **Galera Cluster**
    *   **Tipo:** Open Source
    *   **Función:** Replicación síncrona multi-master para MySQL/MariaDB.
    *   **Notas:** Muy popular para HA real.

6.  **Percona XtraDB Cluster**
    *   **Tipo:** Open Source
    *   **Función:** Basado en Galera, optimizado por Percona.
    *   **Notas:** Excelente para entornos críticos.

7.  **MHA (Master High Availability Manager)**
    *   **Tipo:** Open Source
    *   **Función:** Failover automático para MySQL Replication.
    *   **Notas:** Ligero y confiable.

8.  **Orchestrator**
    *   **Tipo:** Open Source
    *   **Función:** Gestión visual y automática de topologías de replicación.
    *   **Notas:** Muy usado en grandes infraestructuras.

9.  **ProxySQL**
    *   **Tipo:** Open Source
    *   **Función:** Proxy inteligente para balanceo y failover.
    *   **Notas:** Ideal para entornos con múltiples nodos.

10. **Keepalived + HAProxy**
    *   **Tipo:** Open Source
    *   **Función:** Alta disponibilidad a nivel de red y balanceo.
    *   **Notas:** Combinación clásica para HA.
    *   
### 🔁 Funciones de MaxScale para HADR
MaxScale es una solución muy robusta para HADR, situada entre la aplicación y tu cluster MySQL/MariaDB. No es completamente open‑source hoy (BSL), pero ofrece:
***

### ✅ **Herramientas Comerciales**

11. **MySQL Enterprise HA**
    *   **Tipo:** Comercial (Oracle)
    *   **Función:** Alta disponibilidad con soporte oficial.
    *   **Notas:** Incluye herramientas avanzadas y soporte.

12. **ClusterControl (Severalnines)**
    *   **Tipo:** Comercial (con versión limitada gratuita)
    *   **Función:** Gestión centralizada de clusters MySQL/MariaDB.
    *   **Notas:** Automatización completa.
 
