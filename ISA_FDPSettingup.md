# Setting up an ISA compatible FAIR Data Point instance

Author: XiaoFeng Liao
7 Aug 2021

**Abstract**: This document describes how to setting up a FAIR Data Point (FDP) locally to host ISA metadata. The setting up of a FDP hosting ISA metadata generally implemented via two steps. The first step is to deploy the FDP. A local deployment is used in this case. The second step is to configure the FDP so it can host ISA metadata concepts, such as Investigation, Study, Assay and others.



## Step 1. FDP Local Deployment

FAIR Data Point is distributed in Docker images. In our case, a local deployment is used. We follow the instruction at
https://fairdatapoint.readthedocs.io/en/latest/deployment/local-deployment.html

A more complete introduction of FDP can be found at https://fairdatapoint.readthedocs.io/_/downloads/en/latest/pdf/


## Step 2. Deal with ISA metadata
After successfully installed FDP, the next step is to submit metadata to it (in our case, the ISA metadata). As the FDP is DCAT compatible, to host ISA metadata, new resources and shapes should be created to make the FDP ISA compatible.

### 2.1 Define new resources (investigation and study) in FDP

Specifically, we need to define new resources and shapes for Investigation and Study. FDP’s Default resource description layers (metadata) are: 1) Data Repository, 2) Catalog, 3) Resource(Dataset), 4) Distribution, as shown in figure 1:

![Figure 1 : Resources in default setting.](https://github.com/xiaofengleo/FAIRDataCube/blob/main/imgs/fig1.png)

We add two new resources Investigation and Study, by clicking the “Create resource definition” link at the up right of the page. 
First, create Study, fill in the form as figure 2 indicates.

![Figure 2 : Create Study.](https://github.com/xiaofengleo/FAIRDataCube/blob/main/imgs/fig2.png)

For creating Investigation, fill in the form with the content shown in figure 3.

![Figure 3: Create Investigation](https://github.com/xiaofengleo/FAIRDataCube/blob/main/imgs/fig3.png)

After creation of Investigation and Study, the resources page in FDP looks like figure 4:

![Figure 4: New resources defined corresponding to Investigation and Study](https://github.com/xiaofengleo/FAIRDataCube/blob/main/imgs/fig4.png)

### 2.2 Define shapes for Investigation and Study

The next step is to define shapes for Investigation and Study. By choosing the SHALC shapes when clicking the user icon at the up right of the page,  as shown in figure 5.

![Figure 5: Choose SHALC shapes from the menu](https://github.com/xiaofengleo/FAIRDataCube/blob/main/imgs/fig5.png)

The default shapes page looks like figure 6:

![Figure 6: Default shapes page](https://github.com/xiaofengleo/FAIRDataCube/blob/main/imgs/fig6.png)

Click “Create shape” at the top right, a form will be displayed, as shown in figure 7,

![Figure 7: Creation of shape](https://github.com/xiaofengleo/FAIRDataCube/blob/main/imgs/fig7.png)

For Investigation, fill in the Name “Investigation”, and fill in Definition with the shape of Investigation. The detailed shape definition of Investigation can be found in Appendix (A.1). 
For Study, repeat the step, and fill in the form with name “Study” and Definition with the shape of Study.  The detailed shape definition of Study can be found in Appendix (A.2). 
Then, the two new created  shapes Investigation and Study can be seen on the shapes page, as shown in figure 8.

![Figure 8: New created shapes Investigation and Study](https://github.com/xiaofengleo/FAIRDataCube/blob/main/imgs/fig8.png)

To display Investigation at the home page, it is needed to set Investigation as child of  Repository. To do that, edit the Repository from the Resource definition page, add a the Investigation as a child of Repository, as figure 9 indicates.

![Figure 9: Add Investigation as child of Repository.](https://github.com/xiaofengleo/FAIRDataCube/blob/main/imgs/fig9.png)

With all these done, we can now create investigation, click “create” button on the FDP home page, a page for create investigation will appear.
After successfully create an Investigation, we can continue create Studies under the Investigation by clicking the “Create” button.

![Figure 10: The Investigation and Study created.](https://github.com/xiaofengleo/FAIRDataCube/blob/main/imgs/fig10.png)


## Appendix
### A.1: Shape of Investigation
```
@prefix :         <http://fairdatapoint.org/> .
@prefix dash:     <http://datashapes.org/dash#> .
@prefix dcat:     <http://www.w3.org/ns/dcat#> .
@prefix dct:      <http://purl.org/dc/terms/> .
@prefix foaf:     <http://xmlns.com/foaf/0.1/> .
@prefix sh:       <http://www.w3.org/ns/shacl#> .
@prefix dcat-ext: <http://purl.org/biosemantics-lumc/ontologies/dcat-extension/> .

:InvestigationShape a sh:NodeShape ;
  sh:targetClass dcat-ext:Investigation ;
  sh:property [
    sh:path dct:issued ;
    sh:datatype xsd:dateTime ;
    sh:maxCount 1 ;
    dash:viewer dash:LiteralViewer ;
  ], [
    sh:path dct:modified ;
    sh:datatype xsd:dateTime ;
    sh:maxCount 1 ;
    dash:viewer dash:LiteralViewer ;
  ], [
    sh:path foaf:homePage ;
    sh:nodeKind sh:IRI ;
    sh:maxCount 1 ;
    dash:editor dash:URIEditor ;
    dash:viewer dash:LabelViewer ;
  ], [
    sh:name "Investigation PubMed ID" ; 
    sh:path dcterms:identifier ;
    sh:nodeKind sh:IRI ;
    sh:maxCount 2 ;
    dash:editor dash:URIEditor ;
    dash:viewer dash:LabelViewer ;
  ],
  [
    sh:name "Investigation Publication DOI" ; 
    sh:path dcterms:identifier ;
    sh:nodeKind sh:IRI ;
    sh:maxCount 2 ;
    dash:editor dash:URIEditor ;
    dash:viewer dash:LabelViewer ;
  ],
    [
    sh:name "Investigation Publication Author List" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ], 
  [
    sh:name "Investigation Publication Title" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ], 
   [
    sh:name "Investigation Publication Status" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ], 
  [
    sh:name "Investigation Publication Status Term Accession Number" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ], 
  [
    sh:name "Investigation Publication Status Term Source REF" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ], 
  [  sh:name "Investigation Person Last Name" ;
    sh:path foaf:lastName ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  [sh:name "Investigation Person First Name" ;
    sh:path foaf:firstName ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
    [
    sh:name "Investigation Person Mid Initials" ;
    sh:path foaf:firstName ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
 
    [
    sh:name "Investigation Person Email" ;
    sh:path foaf:OnlineAccount ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  
  [
    sh:name "Investigation Person Phone" ;
    sh:path foaf:phone ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  
  [
  sh:name "Investigation Person Fax" ;
    sh:path foaf:phone ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  
  [
  sh:name "Investigation Person Address" ;
    sh:path foaf:phone ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  [
    sh:name "Investigation Person Affiliation" ;
    sh:path foaf:Organization ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  
  [
    sh:name "Investigation Person Roles" ;
    sh:path foaf:Organization ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  
  [
    sh:name "Investigation Person Roles Term Accession Number" ;
    sh:path foaf:Organization ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  
  [
    sh:name "Investigation Person Roles Term Source REF" ;
    sh:path foaf:Organization ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  [
    sh:path dcat:themeTaxonomy ;
    sh:nodeKind sh:IRI ;
    dash:viewer dash:LabelViewer ;
  ] .

```
### A.2: Shape of Study

```
@prefix :         <http://fairdatapoint.org/> .
@prefix dash:     <http://datashapes.org/dash#> .
@prefix dcat:     <http://www.w3.org/ns/dcat#> .
@prefix dct:      <http://purl.org/dc/terms/> .
@prefix sh:       <http://www.w3.org/ns/shacl#> .
@prefix dcat-ext: <http://purl.org/biosemantics-lumc/ontologies/dcat-extension/> .
@prefix sio: <http://semanticscience.org/resource/> . 

:StudyShape a sh:NodeShape ;
  sh:targetClass dcat-ext:Study ;
  sh:property [
    sh:path dct:issued ;
    sh:datatype xsd:dateTime ;
    sh:maxCount 1 ;
    dash:editor dash:DatePickerEditor ;
    dash:viewer dash:LiteralViewer ;
  ], [
sh:path sio:SIO_000001 ;
sh:nodeKind sh:IRI ;
sh:name "is related to" ;
sh:maxCount 1 ;
dash:editor dash:URIEditor ;
dash:viewer dash:LabelViewer ;
],
 [
    sh:name "Study PubMed ID" ; 
    sh:path dcterms:identifier ;
    sh:nodeKind sh:IRI ;
    sh:maxCount 2 ;
    dash:editor dash:URIEditor ;
    dash:viewer dash:LabelViewer ;
  ],
  [
    sh:name "Study Publication DOI" ; 
    sh:path dcterms:identifier ;
    sh:nodeKind sh:IRI ;
    sh:maxCount 2 ;
    dash:editor dash:URIEditor ;
    dash:viewer dash:LabelViewer ;
  ],
    [
    sh:name "Study Publication Author List" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ], 
  [
    sh:name "Study Publication Title" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ], 
   [
    sh:name "Study Publication Status" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ], 
  [
    sh:name "Study Publication Status Term Accession Number" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ], 
  [
    sh:name "Study Publication Status Term Source REF" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ] , 
  [
    sh:name "Study Assay File Name" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Assay Measurement Type" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Assay Measurement Type Term Source REF" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Assay Measurement Type Term Accession Number" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Assay Technology Type" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]   , 
  [
    sh:name "Study Assay Technology Type Term Accession Number" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]   , 
  [
    sh:name "Study Assay Technology Type Term Source REF" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ] , 
  [
    sh:name "Study Assay Technology Platform	U-PLEX" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Protocol Name" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Protocol Type" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Protocol Type Term Accession Number" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Protocol Type Term Source REF" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Protocol Description" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Protocol URI" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Protocol Version" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Protocol Parameters Name" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ]  , 
  [
    sh:name "Study Protocol Parameters Name Term Accession Number" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ] , 
  [
    sh:name "Study Protocol Parameters Name Term Source REF	" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ] , 
  [
    sh:name "Study Protocol Components Name" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ] , 
  [
    sh:name "Study Protocol Components Type" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ] , 
  [
    sh:name "Study Protocol Components Type Term Accession Number" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ] , 
  [
    sh:name "Study Protocol Components Type Term Source REF" ; 
    sh:path dcterms:title ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 2 ;
    dash:editor dash:TextFieldEditor ;
  ],
    [  
  sh:name "Study Person Last Name" ;
    sh:path foaf:lastName ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  [
      sh:name "Study Person First Name" ;
    sh:path foaf:firstName ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
    [
    sh:name "Study Person Mid Initials" ;
    sh:path foaf:firstName ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
    [
    sh:name "Study Person Email" ;
    sh:path foaf:OnlineAccount ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  [
      sh:name "Study Person Phone" ;
    sh:path foaf:phone ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ],  
  [
    sh:name "Study Person Fax" ;
    sh:path foaf:phone ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ], 
  [
    sh:name "Study Person Address" ;
    sh:path foaf:phone ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ],  
  [
    sh:name "Study Person Affiliation" ;
    sh:path foaf:Organization ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ],
  [
    sh:name "Study Person Roles" ;
    sh:path foaf:Organization ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ],
  [
    sh:name "Study Person Roles Term Accession Number" ;
    sh:path foaf:Organization ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ],
  [
    sh:name "Study Person Roles Term Source REF" ;
    sh:path foaf:Organization ;
    sh:nodeKind sh:Literal ;
    sh:maxCount 1 ;
    dash:editor dash:TextFieldEditor ;
    dash:viewer dash:LabelViewer ;
  ] .
```
