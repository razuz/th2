# Rules

## Adding Elastic rules

1. Go to Kibana > Security > Detection Rules (SIEM)
2. Click on Add Elastic Rules
3. Search and select and Install
   * windows
   * linux
4. Select all installed Rules and click on "Bulk Actions" > "Enable"

## Adding Sigma rules

```shell
git clone https://github.com/SigmaHQ/sigma.git
cd sigma
python3 -m venv venv
source venv/bin/activate
pip install sigma-cli
```

### Converting community rules to Elasticsearch

- List which target SIEM solutions can sigma-cli convert to

    ```shell
    sigma plugin list
    ```
- Install the elasticsearch converter

    ```shell
    sigma plugin install elasticsearch
    ```
- Check which formats of Elasticsearch queries are supported (think Lucene or EQL aka SIEM rules)

    ```shell
    sigma list formats lucene
    sigma list formats eql
    ```

- List pipelines aka what field names schema to use

    ```shell
    sigma list pipelines
    ```

- Convert any given Sigma community rule to an Elasticsearch Lucene query where the field names conform to elastic common schema

    ```shell
    sigma convert -t elasticsearch -f default -p ecs_windows rules/windows/process_creation/proc_creation_win_powershell_base64_encoded_cmd.yml
    ```

- Convert Windows Sigma rules for upload and save to a file
    ```shell
    sigma convert -t lucene -p ecs_windows -f siem_rule_ndjson -o /srv/rules/sigma/aws_cloudtrail.ndjson rules/windows/
    ```

- Convert Linux Sigma rules for upload and save into a file on your computer
    ```shell
    sigma convert -t lucene -p ecs_windows -f siem_rule_ndjson -o /srv/rules/sigma/aws_cloudtrail.ndjson rules/linux/
    ```

- Goto Kibana > Rules > SIEM
- Click on "Import Rules"
- Select the file you just created 
  - please note there might be some errors
