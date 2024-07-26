# Overall Architecture
## Sequence Diagram
![Sequence Diagram](http://www.plantuml.com/plantuml/png/lLHHRzis47xNhpXuBocG0Ys6TOCn37Nje0dGsOxiODYW5uOyAqIb8qTILVFlHr8KGbiA1knXBu9uTzzzn-_k-D4wPbpNDaN1k5C67YmQO1Qwub5zXyNcThs70vflagDTm0zVPFtaFZKT5jhZ99UQaHl2AWfnQ1O1Bfwu5dCnNwHrI5bKKo09pvNujeT_fOjH5UsD-lvSKOeUycax4vYNHLOallF0Epefqp8d5LLKOkshDEcK4qXpGR1csiblwAjHnh4c1d5z7lEPEUpPS_JLVL7KHdKQ5eUel8OL3pnsKS2W1xpzRVXPmY0M-D90C_xLvx4LAGBjoU33p-3j7tu9E6qZIjiH0sFKJpzM5F2Ik6ebrH0KDlXtXzRP5wWq7hfcJGEVRuwmsj-1Kr2Z0nErG8C21CQsLFJxQWqh8GnQYqkusuy7Q9dMWQENFj4ZUh3h366KFDqxZLGvL10ktOqN5ak8lesqNFcE9K54y7V9jpkTqCo1Ki8vp8f_9TKtAEeMoLLq5II8qpEEMaLZfS1iHUCGedcJvKjDcSkPjIvJihmv766_Emnwzj8zUQskmQjt3RVAkkkuR6VQUEQ9DB6hcSFRMUFWIfvIHyRKm58RfCtQ5gumjZdE_sKoYDPp8giLMSoHtSI5ZSMy2izAoiqoJ_3JcjK9qYx1i4eHx1CYcF08n2F0Zffdy9MRvo73Rh_URMxW7J0IS7_ySty3x-4gg3iEvPjG6ECSjKFVHb3k2Ost68IiwL36F5lbuAxL3OQkeXX8NueMw9Xix3BP0MwH2JGlPu3x4dvz2-ypIohHMzzbrjNgCkwulemfDvSnvGJrrmGqntQ_MUyUjiTWFh0MWTdn3SXBsaw24YuBsXwYPNATSiPy7mYaeaoVL-bNPFjSoVY39E885F7tR5F-m4VuP5Hl9TMBj1Bo10-KFLYRE9ZUcJQ9woK4N3xxNAVfZ0iFVUxESOTGIsVHZ4EGqFzbvJEeq3FlxaaPZj1fmHpEFC09_ZyysuaeIV0m52J9voNMW3yniCvqt8UZ7P-4ylK6rFsa0TuM6v0SQTFoXd_qtwvj_W40)




# DNS Proxy Server

DNS Proxy Server will maintain in memory cache of all registered devices (MAC address and IP address).

# Registered

## Query Constraints
Only DNS queries with **OPCODE** 0 (Standard Query) and **QTYPE** 1 (Host Address) and **CLASS** 1 (Internet address) will be accepted.

For Others DNS response will be returned with **RCODE** set as `Not Implemented` (4).

## Response Structure
### Header
```
  ID <- Same as request
  QR <- 1
  OPCODE <- 0
  AA <- 1
  TC <- 0
  RD <- 1
  RA <- 1
  Z <- 0
  RCODE <- 0
  QDCOUNT <- Same as request
  ANCOUNT <- Same as QDCOUNT
  NSCOUNT <- 0
  ARCOUNT <- 0
```
### Question
Same as Request

### Answer
```
  NAME <- Same as query
  TYPE <- 1 (A record)
  CLASS <- 1 (Internet address)
  TTL <- 1 or 0 (Very small number to prevent caching)
  RDLENGTH <- 4 (IPv4 address is 4 bytes long)
  RDATA <- IP Address of Captive Portal
```
