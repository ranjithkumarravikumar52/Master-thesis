### A study of social factors in activity-based active learning classroom correlated to students' performance

#### What is this paper about?

In our observational study of students, we formulated and evaluated Group Cohesion score along with its sub-components (Goal Settings, Communication, Trust, Accountability and Recognition), social factors (from open-ended answers) and sentiment analysis (from the LIWC tool).

By taking into consideration our ABAL (activity-based active learning) classroom approach, we provided results correlating these points with academic performance. We found that the Trust trait and three social factors (C1, A1, and R3) collectively had a high and positive correlation with academic performance, while the remaining factors had a less significant correlation. However, when we analyzed data samples with a weekly comparison of student performance against the independent variables, we found no strong correlation.

Please check out the [ProQuest link](https://search.proquest.com/openview/845ddd436ec9148ca974121de5b949a9/1.pdf?pq-origsite=gscholar&cbl=18750&diss=y) for the full published paper, the [thesis PDF](doc/Thesis%20Published.pdf) in this repo, or the [defense slides](doc/Final%20defense.pdf) for a quick overview. **Cheers!**

---

## Contents

- [Installation](#installation)
- [Java Documentation](#java-documentation)
- [Setting up the ELK Environment](#setting-up-the-elk-environment)
- [Elasticsearch API Quick Reference](#some-basic-commands-to-check-status-of-elasticsearch-server)
- [Usage](#usage)
- [Research Questions](#research-questions-i-was-trying-to-solve)
- [Experiment Constraints](#constraints-for-experiment)
- [Credits](#thanks-and-credits)

---

## Installation

- Java JDK 8+
- [Maven](https://maven.apache.org/download.cgi) — manages all Java dependencies automatically
- [Elasticsearch 6.2.4](https://www.elastic.co/downloads/past-releases/elasticsearch-6-2-4) — download and install separately
- [Kibana 6.2.4](https://www.elastic.co/downloads/past-releases/kibana-6-2-4) — download and install separately
- Excel sheet containing the raw survey data

---

#### Build

Run the following to download all dependencies and compile the project:

```bash
mvn compile
```

To produce a runnable JAR:

```bash
mvn package
```

#### Java Documentation

- The project contains two packages: `ParseUtil` and `main`, located under `src/main/java/`
- `ParseUtil` contains two classes — `ElasticSearchServer.java` and `ExcelFile.java`
- In `ElasticSearchServer.java`, update the static variables to set your port number, index name, and document name for Elasticsearch
- In `App.java` (main package), set the name of your Excel file to be parsed

---

#### Setting up the ELK (Elasticsearch Kibana) Environment

1. [Download Elasticsearch 6.2.4](https://www.elastic.co/downloads/past-releases/elasticsearch-6-2-4) and extract it
2. Run Elasticsearch
   - Navigate to `elasticsearch-6.2.4/bin`
   - Run `elasticsearch` (Linux/Mac) or `elasticsearch.bat` (Windows)
   - ![Elasticsearch running](doc/elasticsearch.png?raw=true)
3. [Download Kibana 6.2.4](https://www.elastic.co/downloads/past-releases/kibana-6-2-4) and extract it
4. Run Kibana
   - Navigate to `kibana-6.2.4-<your-platform>/bin`
   - Run `kibana` (Linux/Mac) or `kibana.bat` (Windows)
5. Open Kibana in your browser at `http://localhost:5601`
   - ![Kibana dashboard](doc/kibana.png?raw=true)

---

#### Some basic commands to check status of Elasticsearch server

Run these using `curl` or any HTTP client:

```bash
# List all indices
GET /_cat/indices?v

# Delete an index
DELETE /index-name?pretty

# View documents in the thesis index
GET ranjith-thesis/?pretty

# View all documents in an index
GET ranjith-thesis
```

---

## Usage

1. Download the survey data from Google Sheets as an Excel file and place it in the project's working directory
2. In `App.java`, update the filename to match your Excel file
3. Make sure Elasticsearch and Kibana are running in the background
4. Run `mvn compile` to download dependencies, then run `App.java` — it will parse the Excel file and push each row to Elasticsearch as a JSON document
5. Once the push completes, open Kibana and create visualizations from the indexed data

---

#### Research Questions I was trying to solve

- **RQ1**: What social attributes impact a group member's confidence?
- **RQ2**: How do group members' social attributes affect the group's performance?
- **RQ3**: What are the attributes of socially-isolated members in a group, and what factors lead to a member's isolation?
- **RQ4**: What kinds of social behaviors are generally acceptable or unacceptable by a group?

---

#### Constraints for experiment

1. The goal was to convert data gathered from observational studies (online surveys and direct observation) into visualizations — preferably Kibana
2. All data was collected in Google Sheets over 11–12 weeks from September–November 2017
3. Visualizing the data directly from Google Sheets was difficult to maintain as data was updated regularly
4. The ELK stack solved this by allowing data to be pushed to Elasticsearch and visualized in Kibana continuously
5. This also made it much easier to present findings to others compared to raw spreadsheets

---

#### Thanks and credits

- University of North Carolina at Charlotte
