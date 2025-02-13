![alt text](5fc2847e1bbebc03aa89fbf2-1734532150246.png)

# Introduction

Cyber Threat Intelligence is typically a managerial mystery to handle, with organisations battling with how to input, digest, analyse and present threat data in a way that will make sense. There are numerous platforms that have been developed to tackle the juggernaut that is Threat Intelligence.

## OpenCTI

[OpenCTI](https://github.com/OpenCTI-Platform/opencti) is another open-sourced platform designed to provide organisations with the means to manage CTI through the storage, analysis, visualisation and presentation of threat campaigns, malware and IOCs.

## Objective

Developed by the collaboration of the French National cybersecurity agency (ANSSI), the platform's main objective is to create a comprehensive tool that allows users to capitalise on technical and non-technical information while developing relationships between each piece of information and its primary source. The platform can use the MITRE ATT&CK framework to structure the data. Additionally, it can be integrated with other threat intel tools such as MISP and TheHive.

![alt text](2dea4c51fade0cb08cc810bfef587e69.png)

# OpenCTI Data Model

OpenCTI uses a variety of knowledge schemas in structuring data, the main one being the Structured Threat Information Expression (STIX2) standards. STIX is a serialised and standardised language format used in threat intelligence exchange. It allows for the data to be implemented as entities and relationships, effectively tracing the origin of the provided information.

This data model is supported by how the platform's architecture has been laid out. The image below gives an architectural structure for your know-how.

![alt text](3bbe38f3ae0edf761c9e0541a71d43ff.png)

The highlight services include:

    GraphQL API: The API connects clients to the database and the messaging system.
    Write workers: Python processes utilised to write queries asynchronously from the RabbitMQ messaging system.
    Connectors: Another set of Python processes used to ingest, enrich or export data on the platform. These connectors provide the application with a robust network of integrated systems and frameworks to create threat intelligence relations and allow users to improve their defence tactics.

According to OpenCTI, connectors fall under the following classes:


<table>
<thead>
<tr>
<th>Class</th>
<th>Description</th>
<th>Examples</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>External Input Connector</strong></td>
<td>Ingests information from external sources</td>
<td><span data-testid="glossary-term" class="glossary-term">CVE</span>, <span data-testid="glossary-term" class="glossary-term">MISP</span>, TheHive, <span data-testid="glossary-term" class="glossary-term">MITRE</span></td>
</tr>
<tr>
<td><strong>Stream Connector</strong></td>
<td>Consumes platform data stream</td>
<td>History, Tanium</td>
</tr>
<tr>
<td><strong>Internal Enrichment Connector</strong></td>
<td>Takes in new OpenCTI entities from user requests</td>
<td>Observables enrichment</td>
</tr>
<tr>
<td><strong>Internal Import File Connector</strong></td>
<td>Extracts information from uploaded reports</td>
<td>PDFs, STIX2 Import</td>
</tr>
<tr>
<td><strong>Internal Export File Connector</strong></td>
<td>Exports information from OpenCTI into different file formats</td>
<td>CSV, STIX2 export, PDF</td>
</tr>
</tbody>
</table>

Refer to the connectors and data model documentation for more details on configuring connectors and the data schema.
https://docs.opencti.io/latest/deployment/connectors/
https://docs.opencti.io/latest/deployment/overview/

# OpenCTI Dashboard 1
## OpenCTI Dashboard

Once connected to the platform, the opening dashboard showcases various visual widgets summarising the threat data ingested into OpenCTI. Widgets on the dashboard showcase the current state of entities ingested on the platform via the total number of entities, relationships, reports and observables ingested, and changes to these properties noted within 24 hours.
![alt text](9d315bf643fcd8255663bbc622eafd86.gif)

## Activities & Knowledge

The OpenCTI categorises and presents entities under the Activities and Knowledge groups on the left-side panel. The activities section covers security incidents ingested onto the platform in the form of reports. It makes it easy for analysts to investigate these incidents. In contrast, the Knowledge section provides linked data related to the tools adversaries use, targeted victims and the type of threat actors and campaigns used.

## Analysis

The Analysis tab contains the input entities in reports analysed and associated external references. Reports are central to OpenCTI as knowledge on threats and events are extracted and processed. They allow for easier identification of the source of information by analysts. Additionally, analysts can add their investigation notes and other external resources for knowledge enrichment. As displayed below, we can look at the Triton Software report published by MITRE ATT&CK and observe or add to the details provided.
![alt text](3d69bf61873c80b282699d0484734a15.gif)

## Events

Security analysts investigate and hunt for events involving suspicious and malicious activities across their organisational network. Within the Events tab, analysts can record their findings and enrich their threat intel by creating associations for their incidents.
![alt text](fcf4e0ecfa24b990083eaea63f04ad2e.gif)

## Observations

Technical elements, detection rules and artefacts identified during a cyber attack are listed under this tab: one or several identifiable makeup indicators. These elements assist analysts in mapping out threat events during a hunt and perform correlations between what they observe in their environments against the intel feeds.
![alt text](fe574a56e07500652b12742ec745fdd1.gif)

## Threats

All information classified as threatening to an organisation or information would be classified under threats. These will include:

    Threat Actors: An individual or group of attackers seeking to propagate malicious actions against a target.

    Intrusion Sets: An array of TTPs, tools, malware and infrastructure used by a threat actor against targets who share some attributes. APTs and threat groups are listed under this category on the platform due to their known pattern of actions.

    Campaigns: Series of attacks taking place within a given period and against specific victims initiated by advanced persistent threat actors who employ various TTPs. Campaigns usually have specified objectives and are orchestrated by threat actors from a nation-state, crime syndicate or other disreputable organisation.
![alt text](3114b7173cce09a3b74fbc750d9bff37.png)

## Arsenal

This tab lists all items related to an attack and any legitimate tools identified from the entities.

    Malware: Known and active malware and trojan are listed with details of their identification and mapping based on the knowledge ingested into the platform. In our example, we analyse the 4H RAT malware and we can extract information and associations made about the malware.

    Attack Patterns: Adversaries implement and use different TTPs to target, compromise, and achieve their objectives. Here, we can look at the details of the Command-Line Interface and make decisions based on the relationships established on the platform and navigate through an investigation associated with the technique.

    Courses of Action: MITRE maps out concepts and technologies that can be used to prevent an attack technique from being employed successfully. These are represented as Courses of Action (CoA) against the TTPs.

    Tools: Lists all legitimate tools and services developed for network maintenance, monitoring and management. Adversaries may also use these tools to achieve their objectives. For example, for the Command-Line Interface attack pattern, it is possible to narrow down that CMD would be used as an execution tool. As an analyst, one can investigate reports and instances associated with the use of the tool.

    Vulnerabilities: Known software bugs, system weaknesses and exposures are listed to provide enrichment for what attackers may use to exploit and gain access to systems. The Common Vulnerabilities and Exposures (CVE) list maintained by MITRE is used and imported via a connector.
![alt text](951f356e59e96cd3c9d5c41e7225b32d.gif)

## Entities

This tab categorises all entities based on operational sectors, countries, organisations and individuals. This information allows for knowledge enrichment on attacks, organisations or intrusion sets.
![alt text](307d350963bb1a7dfc0c244014e05815.gif)

# OpenCTI Dashboard 2

## General Tabs Navigation

The day-to-day usage of OpenCTI would involve navigating through different entities within the platform to understand and utilise the information for any threat analysis. We will be looking at the Cobalt Strike malware entity for our walkthrough, mainly found under the Arsenal tab we've covered previously. When you select an intelligence entity, the details are presented to the user through:

    Overview Tab: Provides the general information about an entity being analysed and investigated. In our case, the dashboard will present you with the entity ID, confidence level, description, relations created based on threats, intrusion sets and attack patterns, reports mentioning the entity and any external references.
![alt text](6e2c09b6c897817f6faa45d294ea064c.png)

    Knowledge Tab: Presents linked information associated with the entity selected. This tab will include the associated reports, indicators, relations and attack pattern timeline of the entity. Additionally, an analyst can view fine-tuned details from the tabs on the right-hand pane, where information about the threats, attack vectors, events and observables used within the entity are presented.
![alt text](11499a63b80b9a68223de5f9d321fb3e.gif)

    Analysis Tab: Provides the reports where the identified entry has been seen. The analysis provides usable information about a threat and guides investigation tasks.
![alt text](9e519fa4a57ddb27b972dfee5c8c118b.png)

    
    Indicators Tab: Provides information on IOC identified for all the threats and entities.

    Data Tab: Contains the files uploaded or generated for export that are related to the entity. These assist in communicating information about threats being investigated in either technical or non-technical formats.

    History Tab: Changes made to the element, attributes, and relations are tracked by the platform worker and this tab will outline the changes.

# Scenario

As a SOC analyst, you have been tasked with investigations on malware and APT groups rampaging through the world. Your assignment is to look into the CaddyWiper malware and APT37 group. Gather information from OpenCTI to answer the following questions.

1. What is the earliest date recorded related to CaddyWiper?  Format: YYYY/MM/DD Hint - ESET CaddyWiper March 2022 report
    
    2022/03/15

2. Which Attack technique is used by the malware for execution? Hint - Attack Pattern details under the Knowledge Tab of the entity

    Native API
    ![alt text](image-2.png)

3. How many malware relations are linked to this Attack technique? Hint - See Distribution of Relations details under the Knowledge Tab of the technique

    113
    ![alt text](image-1.png)

4. Which 3 tools were used by the Attack Technique in 2016? (Ans: Tool1, Tool2, Tool3) Hint - Look under Knowledge -> Tools. List tools in alphabetical order.

    BloodHound, Empire, ShimRatReporter
    ![alt text](image-3.png)

5. What country is APT37 associated with? Hint - Check Description of the Intrusion set

    North Korea
    ![alt text](image-4.png)

6. Which Attack techniques are used by the group for initial access? (Ans: Technique1, Technique2)
Hint - Technique codes details found under the Knowledge -> Global Kill Chain

    T1189, T1566
    ![alt text](image-5.png)



