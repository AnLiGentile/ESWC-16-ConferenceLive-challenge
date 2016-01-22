# ESWC-16 Conference Live app Challenge

This folder contains guidelines and materials for the Conference Live app Challenge at [ESWC 2016](http://2016.eswc-conferences.org/).

In the past two years the Extended Semantic Web Conference (ESWC) has provided a semantic Web application to browse conference data. 
The application, called Conference Live, is a Web and mobile application based on conference data from the Semantic Web Dog Food server, which provides facilities to browse papers and authors at a specific conference. The data-backend is provided by the metadata chairs, while the front-end application has been developed by different teams for [ESWC2014](http://oak.dcs.shef.ac.uk/eswc2014) and [ESWC2015](http://oak.dcs.shef.ac.uk/eswc2015). In this challenge we call for a front-end application for ESWC2016. The task consist in implementing a system that allows the navigation of ESWC-16 semantic metadata. The system should satisfy specific requirements indicated in the call. The metadata chairs provide:

- data which is enriched with social features (e.g. integrated Twitter accounts of paper authors), scheduling features (calendar information are attached for paper presentations and social events)
- a backend service to vote for publications, if the conference includes sessions where participants can vote, as it is popular e.g. for poster and demo sessions.


**Submissions** (via [EasyChair](https://easychair.org/conferences/?conf=conferenceliveeswc16)) will consist of:

1. A **summary** description (abstract) of up to 200 words;
2. A **paper** presenting the details of the implemented method, which discusses its novelty (if applicable), and highlights its strengths and weaknesses;
3. **Web Access**: the Web application must be fully implemented and the code must be accessible either via the Web (e.g github) or downloadable. In particular, the application should be:
  - Open Source
  - compatible with [Cordova framework](https://cordova.apache.org/)


# Important Dates

- Challenge **papers** and **systems** submission deadline: Friday March 11th, 2016
- Challenge paper **reviews due**: Tuesday April 5th, 2016
- **Notifications** sent to participants: Friday April 8th, 2016
- Final ESWC 2016 data published (for final test of the winning system): Friday April 8th, 2016
- **Camera ready** papers due: Sunday April 24th, 2016
- [ESWC 2016](http://2016.eswc-conferences.org/) conference: May 29th - June 2nd,ß 2016


The notification will already declare the **winning system**, which will be **distributed by [Conference Live](https://play.google.com/store/apps/developer?id=Conference+Live) as the official ESWC-16 App**. 
If a winning system cannot be proclaimed (e.g. all submissions fail to meet the minimum requisites) the metadata chair will provide a Conference Live baseline system.


# Task Overview

## Task Description

The task consist in implementing a system that allows the navigation of ESWC-16 semantic metadata. The system should satisfy the following requirements:

1. Availability: be Open Source.
2. Implementation: compatible with [Cordova framework](https://cordova.apache.org/).
3. Voting: enable voting for poster and demo through the REST service provided by the organizers (details on the service are provided to participants).
4. Browsing: the system must provide a mechanism to browse papers and authors at the conference. The system will exploit the Linked Data of the conference provided as input for providing effective App-based visualisations of conference related knowledge, including basic information (author names, affiliations, paper titles...), roles covered by each person at the conference and additional data including: author picture, author additional contacts (e.g. social media account), thumbnail for each paper. Additional data might or might not be available for all persons/papers. The system must handle the null cases.
5. Scheduling: the system must provide to the users the conference calendar with the scheduling of events (either social or academic) and paper presentations.
6. Social: provide social functionalities and access to social channels (e.g., Twitter, ResearchGate, etc.) for enabling/improving scholarly net- working and interaction.
7. Proceedings: enable accessing to the conference proceedings
8. Enrichment: enable data enrichment from external and potentially heterogeneous sources. For example, the App could gather authors’ publications and other information related to their scholarly activity (e.g., social accounts or personal webpages) from Open Linked Data or Open Source API.


Requirements 1-5 are essential, a system which doesn’t implement any of these will be disqualified. Requirements 6-8 are preferable and will constitute added value. For implementation examples participants can refer to the systems used at [ESWC2014](http://oak.dcs.shef.ac.uk/eswc2014) and [ESWC2015](http://oak.dcs.shef.ac.uk/eswc2015). For an explanation on meeting the requirements they can refer to [Gentile et al. 2015](∫http://www.www2015.it/documents/proceedings/companion/p1007.pdf).

## Dataset and available services

### Past conference data 
In order to facilitate the system development, we provide data from the past two editions of ESWC.
These data is enriched with social features (e.g. integrated Twitter accounts of paper authors) and scheduling features (calendar information are attached for paper presentations and social events).
Two rdf dumps are available:

  - ESWC-14 metadata from [ESWC2014](./pastConferences_data/eswc2014.rdf)
  - ESWC-15 metadata from [ESWC2015](./pastConferences_data/eswc2015.rdf)

### Voting system 
We provide a backend service to vote for publications. 
The voting service is implemented as a REST service.
To save a user vote, it is sufficient to send a GET query with three parameters: <paper-number> <paper-track> <secret-code> in the form: curl -G -X
GET -d id=PAPER NUMBER -d track=PAPER TRACK -d code=USER SECRET CODE
The <paper-id> is generated internally by the service, concatenating <paper- track> and <paper-number>
- IF the vote is cast correctly the response is an HTTP status code 200, with an extra json file as output, which simply contains the following content "status":"ok"
- IF <secrect-code> has been used already for voting the best paper of a track, there is a CONFLICT ERROR CODE is: HTTP status code 409
- IF either the <paper-id> or the <secrect-code> do not exist ERROR CODE is: HTTP status code 404
- IF there is a syntactic error (parsing of the query string) caused by either the <paper-id> or by the <secrect-code>, there is a PRECONDITION FAILED ERROR CODE is: HTTP status code 412

For testing purposes we provide:
- a voting service for each provided dataset:
  - [ESWC-15](http://wit.istc.cnr.it/eswc2015/vote)
  - [ESWC-14](http://wit.istc.cnr.it/eswc2014/vote)
- a pool of valid secret codes as a [txt file](./voting_resources/voting_tokens.txt). The actual secret codes will be an alpha-numeric string, in the range [a-zA-Z0-9]
- a tool to verify currently saved votes for each provided dataset:
  - [ESWC-15](http://wit.istc.cnr.it/eswc2015/vote/list)
  - [ESWC-14](http://wit.istc.cnr.it/eswc2014/vote/list)


# Evaluation

We will define two evaluations:
- implementation of requirements: the challenge organizers will score each of the requirements with a vote from 0 to 3, where 0 means not implemented, 1 partially implemented, 2 fully implemented, 3 outstanding implementation. The final vote will be a linear combination of the votes for each requirements.
- usability: a goal oriented evaluation will be carried out. Participants will we asked to complete tasks such as finding the time of a presentation, finding the author of a publication, voting for best poster/demo and then complete a questionnaire in order to record the [System Usability Scale (SUS)](http://cui.unige.ch/isi/icle-wiki/_media/ipm:test-suschapt.pdf). The SUS is a metric used for evaluating the usability of a system and it is technology-independent, and reliable even with a very small sample size.
For a system to be evaluated we ask the participants to strictly meet requirement R2 and potentially provide the application already packaged as an Apache Cordova Web App.


# Organising Committee

- [Anna Lisa Gentile](http://dws.informatik.uni-mannheim.de/en/people/researchers/annalisa/), University of Mannheim, Germany
- [Andrea Giovanni Nuzzolese](http://www.cs.unibo.it/~nuzzoles/), STLab-CNR, Italy
- [Valentina Presutti](http://stlab.istc.cnr.it/stlab/User:ValentinaPresutti), STLab-CNR, Italy

# Program Committee

- [Luca Costabello](http://luca.costabello.info/), Fujitsu Linked Data Research Team, Galway, Ireland
- [Mauro Dragoni](http://shell.fbk.eu/people/profile/dragoni), Fondazione Bruno Kessler, Trento, Italy
- [Aldo Gangemi](http://www.istc.cnr.it/people/aldo-gangemi), Université Paris 13, France
- [Suvodeep Mazumdar](http://staffwww.dcs.shef.ac.uk/people/S.Mazumdar), University of Sheffield, UK
- [Lionel Médini](http://liris.cnrs.fr/lionel.medini/), Université Claude Bernard Lyon 1, France
- Christoph Pinkel, fluidOps, Germany
- [Diego Reforgiato](http://www.istc.cnr.it/people/diego-reforgiato-recupero), STLab-CNR, Italy
- [Giuseppe Rizzo](http://giusepperizzo.github.io/), ISMB, Torino, Italy
- [Raphaël Troncy](http://www.eurecom.fr/~troncy/), EURECOM, Sophia Antipolis, France

More to be announced


