# yaml_to_json
Convenience scripts for converting from yaml to json.
Currently my usecase is writing AWS CloudFormation templates in YAML
and then converting them to JSON for the upload to AWS.

Example:

yaml_to_json.json cf.yaml > cf.cftemplate

aws cloudformation create --template-body file://cf.cftemplate
