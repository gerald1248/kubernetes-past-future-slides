---
title: Kubernetes Past and Future 
pdf: kubernetes-past-future-slides.pdf
standalone: kubernetes-past-future-slides.html
transition: slide
backgroundTransition: fade
slideNumber: true
controls: false
controlsTutorial: false
asciinema: true
---

<link href="//netdna.bootstrapcdn.com/font-awesome/4.1.0/css/font-awesome.min.css" rel="stylesheet">

# KUBERNETES PAST AND FUTURE {bgcss=tw-colorful .light-on-dark}

# WHAT DOES KUBERNETES DO? {bgcss=tw-bg-purple .light-on-dark}

# DISTRIBUTED DEPLOYMENT {bgcss=tw-bg-extra-light-blue}

```render_a2sketch
                      #------------#
                      |[c]         |
                      | Users      |
                      |            |
                      #-----#------#
                            |
                            v
                      #-----#------#
                      |[o]         |
                      | Service    | service.namespace.svc.cluster.local
                      |            |
                      #-----#------#
                            |
             #--------------#--------------#
             |                             |
             v              |              v
#------------#------------.   #------------#------------.
|[p]                      | | |[p]                      |
| Pod                     |   | Pod                     |
|                         | | |                         |
#------------#------------.   #------------#------------#
|[w]         |[w]         | | |[w]         |[w]         |
| Container  | Container  |   | Container  | Container  |
|            |            | | |            |            |
#------------#------------#   #------------#------------#
|[w]                      | | |[w]                      |
| Host                    |   | Host                    |
| [zone=a]                | | | [zone=b]                |        
'-------------------------#   '-------------------------#
                            |
Availability zone a           Availability zone b
                            |

[c]: {"a2s:type": "cloud", "a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid", "strokeStyle": "#000"}
[g]: {"a2s:delref": true, "fill": "transparent", "fillStyle": "solid", "strokeStyle": "#000"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[o]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid"}
```

# CANARY DEPLOYMENT {bgcss=tw-bg-yellow}

```render_a2sketch

                      #------------#
                      |[c]         |
                      | Users      |
                      |            |
                      #-----#------#
               95%          |           5%
             #--------------#--------------#
             |                             |
             v                             v
       #-----#------#                #-----#------#
       |[p]         |                |[b]         |
       | v1.0.0     |                | v1.0.1-beta|
       |            |                |            |
       #------------#                #------------#
                             
                             
[c]: {"a2s:type": "cloud", "a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid", "strokeStyle": "#000"}
[g]: {"a2s:delref": true, "fill": "#ddd", "fillStyle": "solid", "strokeStyle": "#000"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
```


# ISOLATED DEPLOYMENT {bgcss=tw-bg-yellow}

```render_a2sketch

                      #------------#
                      |[c]         |
                      | Users      |
                      |            |
                      #-----#------#
                            |
             #--------------#--------------#
             |                             |
             v              |              v
       #-----#------#                #-----#------#
       |[p]         |       |        |[b]         |
       | Service a  |                | Service b  |
       |            |       |        |            |
       #------------#                #------------#
                            |

                     Network policy
                     (layer 3)
                             
[c]: {"a2s:type": "cloud", "a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid", "strokeStyle": "#000"}
[g]: {"a2s:delref": true, "fill": "#ddd", "fillStyle": "solid", "strokeStyle": "#000"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
```

# ZERO TRUST DEPLOYMENT {bgcss=tw-bg-yellow}

```render_a2sketch

                      #------------#       #-----------#    
                      |[c]         |       |[s]        |     
                      | Users      | - - - | Dashboard |     
                      |            |       |           |      
                      #-----#------#       #-----------#      
                            |
             #--------------#--------------#
             |                             |
             v                             v
       #-----#------#                #-----#------#
       |[p]         |                |[b]         |
       | Service a  #<--------------># Service b  |
       |            |  mutual TLS    |            |
       #------------#                #------------#

                       Service mesh  
                       (layer 7)

[c]: {"a2s:type": "cloud", "a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[w]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid", "strokeStyle": "#000"}
[g]: {"a2s:delref": true, "fill": "#ddd", "fillStyle": "solid", "strokeStyle": "#000"}
[s]: {"a2s:type": "computer", "a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
```

# THE COMPETITIVE ENVIRONMENT {bgcss=tw-bg-purple .light-on-dark}

# ALL HAPPY FAMILIES {bgcss=tw-bg-extra-light-blue}

```render_a2sketch
.--------------------------------------------------------------.
|[c]                                                           |
|                             Fleet                            |
|           Docker Swarm                                       |
|                                 OpenShift (1-2)              |
|                      Kubernetes                              |
|     Apache Mesos                                             |
|                             Elastic Container Service        |
|            Heroku                                            |
|                    Cloud Foundry                             |
|                                   Panamax                    |
|          Shipyard                                            |
|                                       Portainer              |
|                                                              |
'--------------------------------------------------------------'

[c]: {"a2s:type": "cloud", "a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
```

<aside class="notes" data-markdown>
Here is a snapshot of the vibrant container scheduler ecosystem just a few short years ago. Note Docker Swarm (still a firm favourite with developers) and Fleet, a container scheduler written by the nascent CoreOS team.
</aside>

# SPLENDID ISOLATION {bgcss=tw-bg-extra-light-blue} 

```render_a2sketch
.--------------------------------------------------------------.
|[c]                                                           |
|                                                              |
|                                                              |
|                                                              |
|                      Kubernetes                              |
|                                                              |
|                                                              |
|                                                              |
|                                                              |
|                                                              |
|                                                              |
|                                                              |
|                                                              |
'--------------------------------------------------------------'

[c]: {"a2s:type": "cloud", "a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
```

<aside class="notes" data-markdown>
However, that is not the ecosystem we have today.

Clearly being the only shark in the fishbowl has helped Kubernetes, but to maintain its position more has to be done.
</aside>

# THE HORCRUX ADVANTAGE {bgcss=tw-bg-purple .light-on-dark}

<aside class="notes" data-markdown>
He Who Must Not Be Named in J.K. Rowling's books has the rather ingenious idea of splitting his soul into many fragments. Each has to be destroyed to get the better of him. This mechanism is meant to make him invincible, and it does prove highly effective. He may not be invincible, but it does take two rather long books to defeat him.
</aside>

# VENDOR SHARDING {bgcss=tw-bg-extra-light-blue}

```render_a2sketch
#-------------------------#   #-------------------------#       
|[p]                      |   |[b]                      |      
|                         |   |                         |      
|      Microsoft          |   |        Red Hat          |       
|                         |   |                         |      
|                         |   |                         |      
#-------------------------#   #-------------------------#       

          #----------------------------------#
          |[c]                               |
          |                                  |
          |              Google              |
          |                                  |
          |                                  |
          #----------------------------------#

#-------------------------#   #-------------------------#       
|[d]                      |   |[e]                      |      
|                         |   |                         |       
|        VMware           |   |        CoreOS           |        
|                         |   |                         |       
|                         |   |                         |       
#-------------------------#   #-------------------------#       

            Cloud Native Computing Foundation
 
[c]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}

```

# PIZZA EFFECTS: IDENTITY {bgcss=tw-bg-extra-light-blue}

```{.render_plantuml args="-Sbackgroundcolor=transparent"}
@startuml
Kubernetes->OpenShift : attribute-based access control (ABAC)
OpenShift->Kubernetes : roles and cluster-roles
Kubernetes->OpenShift : role-based access control (RBAC)
@enduml
```

<aside class="notes" data-markdown>
Since Red Hat embraced Kubernetes for OpenShift 3+, there have been numerous virtuous pizza effects, large and small. RBAC is an example that has worked particularly well.
</aside>

# PIZZA EFFECTS: NETWORKING {bgcss=tw-bg-extra-light-blue}

```{.render_plantuml args="-Sbackgroundcolor=transparent"}
@startuml
Kubernetes->OpenShift : flat network
OpenShift->Kubernetes : multitenant plugin
OpenShift->Kubernetes : prototype network policies
Kubernetes->OpenShift : network policies
@enduml
```

<aside class="notes" data-markdown>
Network policies have arguably been less successful. The question is whether network policies warrant the considerable amount of complexity when placed alongside Red Hat's original `ovs-multitenant` plugin.
</aside>

# PIZZA EFFECTS: STATE {bgcss=tw-bg-extra-light-blue}

```{.render_plantuml args="-Sbackgroundcolor=transparent"}
@startuml
skinparam BoxPadding 10
Kubernetes->OpenShift : beware stateful applications
OpenShift->Kubernetes : application templates (2015)
Kubernetes->Tectonic : stateful applications still hard
Tectonic->Kubernetes : etcd operator with third-party resources (2016)
Kubernetes->Tectonic : Custom Resource Definitions
Tectonic->Kubernetes : Operator Framework and SDK (2018)
Tectonic->OpenShift : merges with (2019)
@enduml
```

<aside class="notes" data-markdown>
</aside>

# THE HORCRUX DILEMMA {bgcss=tw-bg-purple .light-on-dark}

# COMPUTE-1 AND UP {bg=#fff44d}

```render_vegalite
{
    "$schema": "https://vega.github.io/schema/vega-lite/v2.0.json",
    "data": {
        "values": [
            {"regions": 1, "date": "2006", "symbol": "AMZN" },
            {"regions": 1, "date": "2007", "symbol": "AMZN" },
            {"regions": 2, "date": "2008", "symbol": "AMZN" },
            {"regions": 3, "date": "2009", "symbol": "AMZN" },
            {"regions": 4, "date": "2010", "symbol": "AMZN" },
            {"regions": 8, "date": "2011", "symbol": "AMZN" },
            {"regions": 9, "date": "2012", "symbol": "AMZN" },
            {"regions": 10, "date": "2013", "symbol": "AMZN" },
            {"regions": 11, "date": "2014", "symbol": "AMZN" },
            {"regions": 11, "date": "2015", "symbol": "AMZN" },
            {"regions": 16, "date": "2016", "symbol": "AMZN" },
            {"regions": 16, "date": "2017", "symbol": "AMZN" },
            {"regions": 17, "date": "2018", "symbol": "AMZN" },
            {"regions": 0, "date": "2006", "symbol": "GOOG" },
            {"regions": 0, "date": "2007", "symbol": "GOOG" },
            {"regions": 0, "date": "2008", "symbol": "GOOG" },
            {"regions": 0, "date": "2009", "symbol": "GOOG" },
            {"regions": 0, "date": "2010", "symbol": "GOOG" },
            {"regions": 4, "date": "2011", "symbol": "GOOG" },
            {"regions": 6, "date": "2012", "symbol": "GOOG" },
            {"regions": 8, "date": "2013", "symbol": "GOOG" },
            {"regions": 10, "date": "2014", "symbol": "GOOG" },
            {"regions": 12, "date": "2015", "symbol": "GOOG" },
            {"regions": 14, "date": "2016", "symbol": "GOOG" },
            {"regions": 16, "date": "2017", "symbol": "GOOG" },
            {"regions": 18, "date": "2018", "symbol": "GOOG" },
            {"regions": 0, "date": "2006", "symbol": "MSFT" },
            {"regions": 0, "date": "2007", "symbol": "MSFT" },
            {"regions": 0, "date": "2008", "symbol": "MSFT" },
            {"regions": 0, "date": "2009", "symbol": "MSFT" },
            {"regions": 2, "date": "2010", "symbol": "MSFT" },
            {"regions": 8, "date": "2011", "symbol": "MSFT" },
            {"regions": 14, "date": "2012", "symbol": "MSFT" },
            {"regions": 20, "date": "2013", "symbol": "MSFT" },
            {"regions": 26, "date": "2014", "symbol": "MSFT" },
            {"regions": 32, "date": "2015", "symbol": "MSFT" },
            {"regions": 39, "date": "2016", "symbol": "MSFT" },
            {"regions": 46, "date": "2017", "symbol": "MSFT" },
            {"regions": 54, "date": "2018", "symbol": "MSFT" },
            {"regions": 0, "date": "2008", "symbol": "BABA" },
            {"regions": 3, "date": "2009", "symbol": "BABA" },
            {"regions": 3, "date": "2010", "symbol": "BABA" },
            {"regions": 3, "date": "2011", "symbol": "BABA" },
            {"regions": 3, "date": "2012", "symbol": "BABA" },
            {"regions": 3, "date": "2013", "symbol": "BABA" },
            {"regions": 4, "date": "2014", "symbol": "BABA" },
            {"regions": 5, "date": "2015", "symbol": "BABA" },
            {"regions": 9, "date": "2016", "symbol": "BABA" },
            {"regions": 12, "date": "2017", "symbol": "BABA" },
            {"regions": 20, "date": "2018", "symbol": "BABA" }
        ]
    },
    "width": 400,
    "height": 200,
    "mark": "bar",
    "encoding": {
        "x": {
            "timeUnit": "year", "field": "date", "type": "temporal"
        },
        "y": {
            "field": "regions", "type": "quantitative", "scale": {"domain": [0, 120]}
        },
        "color": { "field": "symbol", "type": "nominal", "scale": {
          "domain": [ "AMZN", "GOOG", "MSFT", "BABA" ],
          "range": [ "#fe17bf", "#3364c0", "#27bdce", "#00aa5b" ]
        } }
    },
    "config": {
        "axis": {
            "labelFont": "sans-serif",
            "labelFontSize": 18,
            "titleFont": "sans-serif",
            "titleFontSize": 18
        },
        "axisX": {
            "labelAngle": 0
        },
        "bar": {
            "continuousBandSize": 20
        }
    }
}
```
# VENDOR SPECIFICITY {bgcss=tw-bg-extra-light-blue}

```render_a2sketch
#-------------------------#   #-------------------------#       
|[p]                      |   |[b]                      |      
|                         |   |                         |      
|        Vault            |   |           RDS           |       
|                         |   |                         |      
|                         |   |                         |      
#-------------------------#   #-------------------------#       

          #----------------------------------#
          |[c]                               |
          |                                  |
          |            Kubernetes            |
          |                                  |
          |                                  |
          #----------------------------------#

#-------------------------#   #-------------------------#       
|[d]                      |   |[e]                      |      
|                         |   |                         |       
|        Jenkins          |   |          SQS            |        
|                         |   |                         |       
|                         |   |                         |       
#-------------------------#   #-------------------------#       

                   Amazon Web Services

[c]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}

```

# CLUSTER STATE {bgcss=tw-bg-extra-light-blue}

```render_a2sketch
#------------------------------------------------------------------#
|[q]                                                               |
|                                                                  |
|                                                                  |
|                                                                  |
|    Stateless is Easy, Stateful is Hard.                          |
|                                                                  |
|                                   - Brandon Philips (2016)       |
|                                                                  |
|                                                                  |
|                                                                  |
#------------------------------------------------------------------#

[q]: {"a2s:type": "quote-sw", "a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid"}
```

<div class="tiny">Source: <a href="https://coreos.com/blog/introducing-operators.html">coreos.com/blog/introducing-operators.html</a></div> 

# OPERATORS {bgcss=tw-bg-extra-light-blue}

```render_a2sketch
#--------------------------#     #-------------------------#       
|[p]                       |     |[b]                      |      
|                          |     |                         |      
|Custom Resource Definition+<-+->+        Controller       |       
|  (e.g. "VaultService")   |  |  | (backup, upgrade, etc.) |      
|                          |  |  |                         |      
#--------------------------#  |  #-------------------------#       
                              |
                              |
                              v
                 #------------+-------------#  
                 |[s]                       | 
                 |                          |
                 |                          |
                 |                          | 
                 |   Cluster state (etcd)   |
                 |   Persistent Volumes     |
                 |        ConfigMaps        |
                 |          Secrets         |
                 |                          |
                 #--------------------------#  


[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[s]: {"a2s:type":"storage", "a2s:delref": true, "fill": "#ffffff"}
```

# SPONSORS {bg=#fff44d}

Vault operator<br/>
<img src="assets/img/CoreOS.svg" width="180px"/>

MySQL operator<br/>
<img src="assets/img/Oracle_logo.svg" width="180px"/>

PostgreSQL operator<br/>
<img src="assets/img/Zalando_logo.svg" width="180px"/>

etc.

# VENDOR INDEPENDENCE {bgcss=tw-bg-extra-light-blue}

```render_a2sketch

#-------------------------#   #-------------------------#       
|[p]                      |   |[b]                      |      
|                         |   |                         |      
|     Vault operator      |   |     MySQL operator      |       
|                         |   |                         |      
|                         |   |                         |      
#------------+------------#   #-----------+-------------#       
             |                            |
             v                            v
          #--+----------------------------+--#
          |[c]                               |
          |                                  |
          |            Kubernetes            |
          |                                  |
          |                                  |
          #--#----------------------------+--#
             ^                            ^
             |                            |
#------------+------------#   #-----------+-------------#       
|[d]                      |   |[e]                      |      
|                         |   |                         |       
|   Jenkins X operator    |   |     Kafka operator      |        
|       (Tekton)          |   |                         |       
|                         |   |                         |       
#-------------------------#   #-------------------------#       

      Any cloud offering a managed Kubernetes service 

[c]: {"a2s:delref": true, "fill": "#fff", "fillStyle": "solid"}
[p]: {"a2s:delref": true, "fill": "#ef5ba1", "fillStyle": "solid", "strokeStyle": "#000"}
[b]: {"a2s:delref": true, "fill": "#f99c41", "fillStyle": "solid", "strokeStyle": "#000"}
[d]: {"a2s:delref": true, "fill": "#27bdce", "fillStyle": "solid", "strokeStyle": "#000"}
[e]: {"a2s:delref": true, "fill": "#00aa5b", "fillStyle": "solid", "strokeStyle": "#000"}
```

# <small>THANK YOU</small> {bgcss=tw-colorful .light-on-dark}
<small>Slides built with <a href="https://github.com/arnehilmann/markdeck">Markdeck</a><br/>
<i class="fa fa-github" aria-hidden="true" style="vertical-align: middle"></i> <a href="https://github.com/gerald1248/who-needs-users-slides">gerald1248/kubernetes-past-future-slides</a><br/>
<i class="fa fa-twitter" aria-hidden="true" style="vertical-align: middle"></i> 03spirit</small>
