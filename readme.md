# A study of social factors in activity-based active learning classrooms correlated to students' performance

## What is this paper about?

In our observational study of students, we formulated and evaluated a Group Cohesion score along with its sub-components (Goal Settings, Communication, Trust, Accountability, and Recognition), social factors (from open-ended answers), and sentiment analysis (from the LIWC tool).

By taking into consideration our ABAL (activity-based active learning) classroom approach, we provided results correlating these points with academic performance. We found that the Trust trait and three social factors (C1, A1, and R3) collectively had a high and positive correlation with academic performance, while the remaining factors had a less significant correlation. However, when we analyzed data samples with a weekly comparison of student performance against the independent variables, we found no strong correlation.

Please check out the [ProQuest link](https://search.proquest.com/openview/845ddd436ec9148ca974121de5b949a9/1.pdf?pq-origsite=gscholar&cbl=18750&diss=y) for the full published paper, the [thesis PDF](doc/Thesis%20Published.pdf) in this repo, or the [defense slides](doc/Final%20defense.pdf) for a quick overview.

---

## Contents

- [Prerequisites](#prerequisites)
- [Build](#build)
- [Project Structure](#project-structure)
- [ELK Stack Setup](#elk-stack-setup)
- [Elasticsearch API Quick Reference](#elasticsearch-api-quick-reference)
- [Usage](#usage)
- [Research Questions](#research-questions)
- [Experiment Constraints](#experiment-constraints)
- [Credits](#credits)

---

## Prerequisites

- Java JDK 8+
- [Maven](https://maven.apache.org/download.cgi) — manages all Java dependencies automatically
- [Elasticsearch 6.2.4](https://www.elastic.co/downloads/past-releases/elasticsearch-6-2-4) — download and install separately
- [Kibana 6.2.4](https://www.elastic.co/downloads/past-releases/kibana-6-2-4) — download and install separately
- An Excel file containing your survey/observational data (not included in this repo)

---

## Build

Run the following once to download all dependencies and compile the project:

```bash
mvn compile
```

After that, open the project in any Java IDE (IntelliJ IDEA, Eclipse, VS Code with the Java extension) and run `App.java` directly from the IDE. The compiled classes will be in `target/classes/`.

---

## Project Structure

```
src/main/java/
├── main/
│   └── App.java                  # Entry point — set your Excel filename here
└── ParseUtil/
    ├── ElasticSearchServer.java  # HTTP client that pushes JSON to Elasticsearch
    └── ExcelFile.java            # Reads .xlsx files and converts rows to JSON
```

**Configuration before running:**

- In `ElasticSearchServer.java` — update the static variables for your port, index name, and document name
- In `App.java` — update the filename to match your Excel file

---

## ELK Stack Setup

1. [Download Elasticsearch 6.2.4](https://www.elastic.co/downloads/past-releases/elasticsearch-6-2-4) and extract it
2. Start Elasticsearch:
   - Navigate to `elasticsearch-6.2.4/bin`
   - Run `./elasticsearch` (Linux/Mac) or `elasticsearch.bat` (Windows)
   - Verify it's running at `http://localhost:9200`
   - ![Elasticsearch running](doc/elasticsearch.png?raw=true)
3. [Download Kibana 6.2.4](https://www.elastic.co/downloads/past-releases/kibana-6-2-4) and extract it
4. Start Kibana:
   - Navigate to `kibana-6.2.4-<your-platform>/bin`
   - Run `./kibana` (Linux/Mac) or `kibana.bat` (Windows)
5. Open Kibana at `http://localhost:5601`
   - ![Kibana dashboard](doc/kibana.png?raw=true)

---

## Elasticsearch API Quick Reference

These are REST API calls — run them via **Kibana's Dev Tools console** (`http://localhost:5601/app/kibana#/dev_tools`) or with `curl`:

```
# List all indices
GET /_cat/indices?v

# Delete an index (replace <your-index> with your index name)
DELETE /<your-index>?pretty

# View index metadata
GET /<your-index>?pretty

# View all documents in an index
GET /<your-index>/_search?pretty
```

Using `curl`:

```bash
# List all indices
curl http://localhost:9200/_cat/indices?v

# View all documents
curl http://localhost:9200/<your-index>/_search?pretty
```

---

## Usage

1. Export your survey/observational data from Google Sheets as an `.xlsx` file and place it in the project's root directory
2. In `App.java`, set the filename to match your Excel file
3. In `ElasticSearchServer.java`, set the index name and document type to match your study
4. Make sure Elasticsearch and Kibana are running (see [ELK Stack Setup](#elk-stack-setup))
5. Run `mvn compile` to download all dependencies, then run `App.java` from your IDE
6. Once the data is pushed, open Kibana and use **Discover** to browse your data and **Visualize** to build charts

---

## Research Questions

- **RQ1**: What social attributes impact a group member's confidence?
- **RQ2**: How do group members' social attributes affect the group's performance?
- **RQ3**: What are the attributes of socially-isolated members in a group, and what factors lead to a member's isolation?
- **RQ4**: What kinds of social behaviors are generally acceptable or unacceptable by a group?

---

## Experiment Constraints

1. The goal was to convert data from observational studies (online surveys and direct observation) into visualizations — preferably using Kibana
2. All data was collected in Google Sheets over 11–12 weeks from September–November 2017
3. Visualizing data directly from Google Sheets was difficult to maintain as it was updated regularly
4. The ELK stack allowed data to be pushed continuously to Elasticsearch and visualized in Kibana
5. This also made it much easier to present findings compared to raw spreadsheets

---

## Credits

- University of North Carolina at Charlotte
