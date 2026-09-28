# EcoPile Expert

EcoPile Expert is a rule-based expert system for diagnosing common home-composting problems. It was developed in SWI-Prolog and contains 25 source-backed production rules.

The system asks the user questions about a compost pile, including its moisture, odor, temperature, ingredients, pest activity and readiness. It then identifies possible problems and recommends corrective actions.

## Main Features

- 25 IF-THEN expert-system rules
- Interactive command-line interface
- Multiple diagnoses can be produced in one assessment
- Explanation of every fired rule
- Preventive recommendations
- Knowledge-source references
- Derived facts
- Automated tests using SWI-Prolog PlUnit
- Input validation for menu questions

## Technologies

- SWI-Prolog 10.0.2
- SWI-Prolog PlUnit

## Requirements

Install the stable 64-bit version of SWI-Prolog:

https://www.swi-prolog.org/download/stable

Verify the installation with:

```powershell
swipl --version
```

The system was developed using:

```text
SWI-Prolog version 10.0.2 for x64-win64
```

## Running the System

Open a terminal inside the project directory and run:

```powershell
swipl -q -s main.pl
```

The system will display a series of numbered questions.

After all questions have been answered, the system displays every matching diagnosis and recommended action.

## Running the Automated Tests

Run:

```powershell
swipl -q -s test_system.pl -g run_tests -t halt
```

The tests check:

- The knowledge base contains exactly 25 rules
- Rule IDs are unique
- Every rule contains conditions
- Every rule has a valid knowledge source
- Derived facts are generated correctly
- Dry-pile diagnosis
- Excess-moisture diagnosis
- Odor diagnosis
- Heating problems
- Unsuitable compost materials
- Pest problems
- Finished-compost identification
- Normal pile with no warning


## Rule Categories

| Category | Rule IDs | Purpose |
|---|---|---|
| Moisture | R01, R02, R09, R11, R12 | Identifies dry or excessively wet conditions |
| Odor | R03, R04, R05 | Identifies causes of unusual odors |
| Temperature | R06, R07, R08 | Identifies why a pile is not heating |
| Aeration and balance | R10, R13 | Identifies airflow and material-balance problems |
| Unsuitable materials | R14–R20 | Detects materials that should be avoided |
| Pest management | R21–R24 | Identifies possible causes of animals and flies |
| Compost readiness | R25 | Determines whether compost appears ready |

## Knowledge Sources

The rules were not generated as unsupported personal opinions. They were derived from the following published sources.

### United States Environmental Protection Agency

**Composting At Home**

https://www.epa.gov/recycle/composting-home

Used for guidance concerning moisture, aeration, heating, brown and green materials, unsuitable materials, rodents and finished-compost characteristics.

### Cornell University

**Troubleshooting Composting Problems**

https://compost.css.cornell.edu/trouble.html

Used for troubleshooting insufficient heat, excessive moisture, odor, pile size, nitrogen balance and animal attraction.

### Cornell University

**Monitoring Compost Odors**

https://compost.css.cornell.edu/monitor/monitorodor.html

Used for ammonia, musty and sulfurous odor diagnoses.

### Oregon State University Extension Service

**Make Compost That Really Cooks: Troubleshoot Heat, Odor and Pests**

https://extension.oregonstate.edu/news/make-compost-really-cooks-troubleshoot-heat-odor-pests

Used for pile-size, rotten-egg odor, rain protection and wildlife recommendations.

## Scope

EcoPile Expert is intended for ordinary home and backyard compost piles.

It is not designed for:

- Industrial composting facilities
- Hazardous-waste treatment
- Medical-waste treatment
- Commercial regulatory compliance
- Laboratory analysis
- Replacing advice from environmental authorities
