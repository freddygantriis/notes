---
Link: https://dagster.io/blog/what-dagster-believes-about-data-platforms
---
```table-of-contents
style: nestedList # TOC style (nestedList|inlineFirstLevel)
minLevel: 0 # Include headings from the specified level
maxLevel: 0 # Include headings up to the specified level
includeLinks: true # Make headings clickable
debugInConsole: false # Print debug info in Obsidian console
```

Summary of beliefs:
- **Data engineering is software engineering** – A modern software engineering workflow, where all logic is captured as code or configuration in a version-controlled repository, is the best way to develop and manage data pipelines.
- **Data platforms are heterogeneous** – Each data platform needs to accommodate a variety of data storage and processing tools.
- **Data platforms should be monolithic** – There should be one data platform per organization, not one per team. The benefits of wide access to data, a standardized metadata and control plane, and data platform leverage are worth the costs of integrating everyone underneath a single roof.
- **Declarative > imperative** – Explicitly defining data assets and the state they should be in is the best way to tame the chaos that naturally arises in data platforms.

## What is a data platform?
I korte træk er en data platfrom basically en platform der får noget data ind, som jeg opbevares, processeres, præsenteres, analyseres osv. Det er altså et fagterm for en samling af teknologier og enheder der er forbundet til at behandler data på en eller anden måde. 

Det kan altså være at man har et sted man opbevare data-en, som en anden platform kan hente og bearbejde og derefter kan det ryge videre til en eller anden form for visualiserings-værktøj, hvor man kan analysere data-en. 

Eksempel som er nævnt i artiklen:

> Every organization that has data has a data platform. Google Sheets can be an effective way to store and process data in some circumstances – but some data platforms are more developed than others. Even among developed data platforms, there’s significant variation in tools and practices.

## The Dagster Approach to Data Platforms
#### Data engineering is software engineering
Det første der bliver nævnt, er at _data engineering is software engineering_.

Det vil sige, at de mener at:
- Data pipelines are expressed as code, checked into a shared version control system like git.
- Changes are vetted in a staging or test environment before being deployed to production.

Årsagen til dette, er, at de mener at kode er utrolig fleksibelt, så man kan tilpasse det præcist til ens behov, og minimere mængden af redundans, fordi man hele tiden kan genbruge kode-elementer forskellige steder.

Dertil mener de også, at man ikke skal bruge _drag & drop_ tools, da de er meget gode til at komme i gang, men det kan blive rigtig bøvlet at vedligeholde i fremtiden, fordi man ikke kan tilpasse det præcist efter ens behov.

#### Data platforms are heterogeneous
Det næste segment omhandler så _Data platforms are heterogeneous_. Det betyder at dataplatforme skal kunne indholde mange forskellige typer af opbevaringsystemer og processeringsteknologier.

De deler heterogenitet op i to dele: _technological and organisational heterogeneity_.

_Technological heterogeneity_ betyder i al sin enkelthed, at en dataplatform skal kunne tilpasse sig mange forskellige typer at teknologier. Dels fordi en teknologi der er god til at indsamle data, er ikke nødvendigvis god til at processere data. Dertil kan den teknologi der bedst til en ting i dag, bliver forældet og andre teknologier kan blive meget bedre i fremtiden.

_Organisational heterogeneity_ betyder derimod, at en dataplatform skal kunne tilpasse sig mange forskellige behov fra forskellige dele af en organisation. Så lidt lignende den forrige definition, men hvor her er der fokus på at en dataplatform både skal kunne understøtte marketing, ML team, økonomi-afdeling osv.

#### Data Platforms Should Be Monolithic
Dette segment handler om at der kun skal være en enkelt dataplatform for hele virksomheden. 

Årsagen til dette er:
- _Business alignment_: Alle arbejder udfra den samme data så man undgår at der opstår modsættene meninger. Så hvis to afdelinger skal arbejde sammen, kan de let arbejde ud fra den samme data, og dermed lettere udføre deres arbejde tilfredsstillende.
- _Data Productivity_: Vi undgår redundans i form af at alle teknologier hænger sammen i den samme data platform, og så kan man også drage fordel af at en afdeling kan analysere data som en anden afdeling træffer sine beslutninger ud fra.
- _More leverage and more consistency_: Hver afdeling skal ikke selv holde styr på deres egen data, men man kan sørge for at der er et _platform team_ der sørger for at data platformen fungerer for hele virksomheden. Og brugere der skifter afdeling eller debugger på tværs af en pipeline skal ikke lære nye teknologier hver gang.

![[What Dagster Believes About Data Platforms 1.png]]
Note: En person kan være 
#### Declarative > Imperative
Det der menes med _declarative > imperative_ er i bund og grund, at man ikke skal tænke hvad der skal ske med data-en i næste step, men derimod hvilket slut-stadie data skal ende i. Skal det ende i en database, eller skal det visualisere i form af et diagram osv. 

Så hvis man tænker _imperative_ så tænker man i hvilken handling der skal ske næste gang i.e. "ændre x". Derimod, hvis man tænker _declarative_ så tænker man "Der skal være en tabel med data fra kilde x".

At være _declarative_ tager lidt mere tid i starten, da man skal deklarere præcist hvad man skal bruge data-en til. Man tænker altså ikke længere i hvad der skal ske med data-en, men nærmere hvordan data-en skal bruges af virksomheden, og hvordan den relatere sig til andre pipelines i data platformen. Det er lidt mere arbejde på kortsigt, men meget mindre arbejde på langsigt.

## Dagster's Design Principles

#### Center the assets
_Data Asset_: Det er term der beskriver ethvert objekt i _persistent storage_ der indsamler noget viden om verdenen.

Meningen med termet _center the assets_ er, at man hele tiden tager udgangspunkt i hvilke _data assets_ man bruger og hvilke man producere. For alle pipeline gør brug af nogle _data assets_ og producere nogle nye.

Dagter er derfor designet efter at brugeren hele tiden tænker på deres _data assets_ i hvert stadie af en given pipeline:

>When defining data pipelines using Dagster’s APIs, users start by declaring the assets that their pipelines operate on and the dependencies between them. Dagster’s UI revolves around the data asset graph, which makes it straightforward to track problems by starting from the impacted data and debugging backwards to the computations responsible for producing that data.

![[What Dagster Believes About Data Platforms 2.png]]

Dagster er designet på _Software-defined Asset Abstraction_.

TODO: Læs artiklen https://dagster.io/blog/software-defined-assets

#### Code is King
Som nævnt tidligere er den bedste måde at designe pipelines på med kode, så for at bygge pipelines i Dagster, skal man redigere og _deploy_ kode. Ikke nogen _drag & drop_ eller UI-redigering.

Al logik i ens pipeline - altså hvad der skal ske i hvert stadie af ens pipeline - skal derfor skrives i kode.

Dagsters rolle i verden er ikke at bygge dine pipelines, men derimod at løse nogle af de problemer der kan opstå når man har en _code-centric_ pipeline.

- Its streamlined decorator-based APIs enable defining pipelines without extraneous boilerplate.
- Rich logging and observability make it easier to understand what happens when Dagster executes user code.
- Dagster Cloud’s built-in Github Actions aid with packaging and deploy code.
- For those who don’t want to host any orchestration infrastructure, Dagster Serverless fully automates packaging and deploying code.

#### Embrace Non-production Environments
Hovedpointen her, er, at de tror på, at hvis man kører hele - eller dele af - ens pipeline lokalt, så kan man i højere grad sikre sig at man ikke sætter en masse fejl i produktion. Så både at man kan teste det lokalt ved at køre det, men også at man kan lave en test suite der beskriver hvordan man regner med at hver del af ens pipeline burde agere. På den måde sørger man også for at man fanger fejl i ens pipeline, hvis man tilføjer eller ændre dele af den.

Dagster features:
- You can work with all Dagster objects inside unit tests and notebooks. The [direct invocation](https://docs.dagster.io/concepts/assets/software-defined-assets#testing) and [in-process execution](https://docs.dagster.io/concepts/testing#testing-a-job-execution) APIs enable execution without spinning up any long-running processes.
- Dagster’s [resource](https://docs.dagster.io/concepts/resources#resources) and [I/O manager](https://docs.dagster.io/concepts/io-management/io-managers#io-managers) abstractions make it easier to test pipelines without overwriting production data.
- The [`dagster dev` command](https://docs.dagster.io/_apidocs/cli#dagster-dev) enables an iterative local pipeline development workflow without launching any infrastructure.
- [Dagster Cloud branch deployments](https://docs.dagster.io/dagster-cloud/managing-deployments/branch-deployments) enable every pull-request to be accompanied by a staging environment that contains the pipelines as defined in that branch.

#### Multi-Tenancy From Day One

>Good Fences make good neighbours

Det er vigtigt at man tænker på, at dataplatformen skal kunne bruges af mange forskellige teams, og der er derfor også mange forskellige teams der er afhængige af at hele alle pipelines fungerer. Eventuelle problemer kunne opstå ved:
- _Starvation_: En pipeline bruger alle ressourcerne der er tilgængelige, hvilket betyder at andre pipelines ikke kan fungere optimalt.
- _Monolithic Dependencies_: At man regner med at alt kode i ens data-platform har de samme biblioteker til rådighed, eller at de har de samme versioner til rådighed.
- _Coupled Failures_: Et problem med en pipeline påvirker andre pipelines. F.eks. hvis en pipeline ikke kan bearbejde data, er det svært for en anden pipeline at analysere det.

Dagster features:
- Dagster _[code locations](https://docs.dagster.io/concepts/code-locations#code-locations)_ enable teams within a Dagster deployment to have fully separate library dependencies, including different versions of Dagster itself.
- Code locations also defend against starvation and coupled failures: even if code can’t be loaded, or if one teams schedules take too long to evaluate, other teams won’t be affected.
- Dagster has rich functionality for separating work into queues and applying per-queue rate limits.
- Dagster’s Software-Defined Asset APIs encourage a federated approach to defining pipelines. Instead of encouraging monolithic DAG definitions, each data asset can function as its own independent unit, with its own data dependencies and its own criteria for when it should be automatically updated

## From Beliefs to Practice
Dette afsnit omhandler i bund og grund, at for at se disse principper blive brugt, bliver man nød til at skifte sin tanke fra "hvad er det letteste?" til "hvad er det rigtige at gøre?". Altså:
- Asking teams to come together and standardize on cross-cutting tools and practices, rather than each team using what’s easiest for them in the moment.
- Writing pipelines in code and checking them into version-control systems, rather than using drag-and-drop tools.
- Writing pipelines in a way that declares their purpose, rather than writing the shortest piece of code that gets the job done.
Med andre ord, så tænk langsigtet fremfor kortsigtet. 