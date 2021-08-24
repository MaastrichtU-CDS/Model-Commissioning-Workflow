# FAIRcomml software package

This repository contains the execution environment for the FAIRcomml software package.

## Prerequisites:
- Docker CE (for Windows/macOS optionally)

## How to install?
1. Download this repository [here](https://github.com/MaastrichtU-CDS/Model-Commissioning-Workflow/archive/refs/heads/master.zip), or clone the repository using the command `git clone https://github.com/MaastrichtU-CDS/Model-Commissioning-Workflow.git`.
2. Please run the command `docker-compose up -d`. This will download and install all components needed (docker containers).
If needed, you can store your own CSV dataset in [./triplifier_data](./triplifier_data) folder. This data will be parsed and stored in the RDF store.

## How to use?
You can view and select all available prediction models at [http://localhost:8080](http://localhost:8080). Specific properties of these prediction models are available, and a validation request can be posted for a specific prediction model.

The data administrators have a separate user interface to review validation requests which need a (sparql) query on the FAIR data point. This user interface is available at [http://localhost:5000](http://localhost:5000). An example query is included below:
```
PREFIX xsd: <http://www.w3.org/2001/XMLSchema#>
PREFIX dbo: <http://um-cds/ontologies/databaseontology/>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX data: <http://triplifier.local/rdf/ontology/>

select ?tableRow (xsd:int(?cTval) as ?cT) (xsd:int(?cNval) as ?cN) ?tLength (xsd:int(?pCRval) as ?ypT0N0)
where {
  ?tableRow rdf:type data:thunder.
  ?tableRow dbo:has_column [
      rdf:type data:thunder.cT;
      dbo:has_cell [
        dbo:has_value ?cTval;
      ];
  ];
        dbo:has_column [
      rdf:type data:thunder.cN;
      dbo:has_cell [
        dbo:has_value ?cNval;
      ];
  ];
        dbo:has_column [
      rdf:type data:thunder.pCR;
      dbo:has_cell [
        dbo:has_value ?pCRval;
      ];
  ].
  BIND (xsd:double(7.5) as ?tLength).
}
```

Afterwards, the system will process the valiation request, and perform the model validation. Validation results will be stored in the RDF database as well, and will be made visible in the main user interface (for model selection).