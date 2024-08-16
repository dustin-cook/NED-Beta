# NED-Beta
Nonstructural Element Database - Beta version for internal development

## Overview
This repository serves as a temporary hosting and version control for the initial development of NED, the Nonstructural Element Database to support building-specific seismic performance research and assessment. NED acts as a relational database that collects information from experimental, anayltical, and historic performance observations of nonstructural building elements into seismic fragilities and consequence models for use in Performance-Based Earthquake Engineering. 

## Expected Final Product
Once initial development is nearing completion, this Github repository will be replaced with a stable, web-deployed SQL database and GUI for use by engineers and researchers. The database will contain component response and damage observations from past experimental seismic tests of nonstructural building components and an extensive set of nonstructural seismic fragilities models. The experimental data and seismic fragility data will be explicitly related and implemented in a SQL format. The database will be documented and published alongside integrated Jupyter notebooks that help illustrate data interaction and visualization for future users.  

## Data Schema
### Component Subcategorization Hierarchy
To categorize building components, we rely on the UNIFORMAT II element classification system (NISTIR 6389). However, this system only classifies nonstructural components at a high level, and further detail is needed to adequately separate different types of components within each category for the purpose of assessing building performance.  Therefore, we propose a new subcategorization hierarchy consisting of four nested component attributes:
-	**Layer 1: Component Subtype** - Describes the major subgrouping of components within the NISTIR class. Can separate full system tests from individual components tests, or major types of components like full height from partial height walls. 
-	**Layer 2: Connection Detail** – Describes the specific type of installation or connection type of the component, such as perimeter-fixed vs back-braced ceilings.
-	**Layer 3: Material Class** – Describes a general grouping of components based on material, i.e., light weight vs heavy weight ceiling tiles or CPVC vs iron sprinkler pipes.
-	**Layer 4: Size Class** - Describes a general grouping of components based on size, i.e., large gridded area of ceiling tiles or specific equipment size.

![image](https://github.com/user-attachments/assets/ed66e51b-b4ed-4e45-9cf5-e4626c9a183a)

The purpose of the component subcategorization is to provide further structured detail to end users who use the collected data for fragility development. When populating data attributes, not all subcategorization layers need to be assigned if they are not applicable. Also, consistent naming, case, and spelling schemes should be used when populating subcategorization attributes. Reviewers should review the Sweets MasterFormat construction products database to familiarize themselves with general component taxonomy and terminology prior to developing subcategorization hierarchies for particular component types.

### DS Class
To provide a structured detail of observed damage attributes, we propose a DS Class attribute consisting of the possible mutually exclusive classifications: 
-	**No damage**: no change in state was observed from the test.
-	**Inconsequential Damage**: (aesthetic) damage was observed but is unlikely to require repair or impact system operation (no action required). E.g., if the component was hidden would the building user ever know there was a problem? Or would the building performance be affected in any way? 
-	**Consequential Damage**: May require repair or impact system operation (observable and requires action).

![image](https://github.com/user-attachments/assets/b9f4a4bd-3083-4028-bc7b-dba06b1f3dd0)

The purpose of the DS Class attributes is to provides a first-pass structured grouping of observed damage to aid in later fragility development. However, we recognize that any grouping of damage states introduced subjectiveness into the process. Therefore, our goal is to implement as little subjectiveness as possible while still providing useful structured data for later users of the database.  This attributes simply acts to separate consequential damage from inconsequential damage. Further separation of consequential damage into multiple damage states is an attribute of the damage state itself and not the initial observation of damage and is therefore up to the fragility developer to refine. 

All observations of damage in the database are assigned into one of the three aforementioned DS classes; if for some reason a damage state class cannot be identified by the reviewer, it should be flagged as “unknown”. When in doubt, we err towards assigning observed damage as consequential, to allow the later fragility developers the option to decide whether or not to include the observation in their fragility development.


