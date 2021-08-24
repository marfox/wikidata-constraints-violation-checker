# Wikidata Constraints Violation Checker

The Wikidata Constraints Violations Checker allows you to analyze the number of constraints violations on a list of Wikidata Items. This is useful to better understand which Items need improvements the most and to better understand the data quality of a specific area of Wikidata.

## Installation
This script requires at least Python 3.6. In your terminal, run:

```bash
git clone https://github.com/wmde/wikidata-constraints-violation-checker.git
cd wikidata-constraints-violation-checker
pip3 install -r requirements.txt
```

## Usage

```bash
# To run the script with an input file
python3 checkDataQuality.py -i <inputfile>

# To run the script using randomly generated Item IDs
python3 checkDataQuality.py -r <number of items>

# You can also specify an output filename
python3 checkDataQuality.py -i <inputfile> -o <outputfile>

# Or a batch size
python3 checkDataQuality.py -r <number of items> -b <batch-size>
```

| Arg | Name                    | Description                                                                            |
| :-: | ----------------------- | -------------------------------------------------------------------------------------- |
| -i  | Input file              | The path to the file containing the input data                                         |
| -r  | Randomly generate Items | The number of Items to randomly generate                                               |
| -o  | Output file             | The path to the file for output                                                        |
| -b  | Batch Size              | The list of Items are broken down into batches for processing. <br>Default value is 10 |

## Input Data

The script can read CSV files or generate random Item IDs.

### CSV File

Example input file, the first column will be used to query for constrains violations:

```csv
Q60,New York
Q64,Berlin
Q70,Bern
Q84,London
Q90,Paris
```

## Output Data

The following fields are provided in the output data for Items that are succesfully checked.

|            Field            | Description                                                                                                                    |
| :-------------------------: | ------------------------------------------------------------------------------------------------------------------------------ |
|             QID             | The unique Item identifier                                                                                                     |
|         statements          | Total amount of statements on the Item                                                                                         |
| violations_mandatory_level  | # of violations at a [mandatory level](https://www.wikidata.org/wiki/Wikidata:2020_report_on_Property_constraints#mandatory)   |
|   violations_normal_level   | # of violations at a [normal level](https://www.wikidata.org/wiki/Wikidata:2020_report_on_Property_constraints#normal)         |
| violations_suggestion_level | # of violations at a [suggestion level](https://www.wikidata.org/wiki/Wikidata:2020_report_on_Property_constraints#suggestion) |
|     violated_statements     | # of statements with violations                                                                                                |
|       total_sitelinks       | # of sitelinks on the Item                                                                                                     |
|     wikipedia_sitelinks     | # of sitelinks to Wikipedia                                                                                                    |
|         ores_score          | [ORES Item quality score](https://www.wikidata.org/wiki/Wikidata:Item_quality) <br>From 1 to 5 (lowest to highest)                                                 |

## Note

Please be aware that some large Items are skipped during the analysis because the constraint check API times out for them.
