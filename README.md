# yaml_to_json
Convenience scripts for converting from yaml to json.
Currently my usecase is writing AWS CloudFormation templates in YAML
and then converting them to JSON for the upload to AWS.

Two implementations are included: Ruby and Python.

The advantage of writing CloudFormation templates in YAML over JSON is that
YAML allows for comments. Also, in my option, YAML is far for readable than
JSON. Since CloudFormation requires JSON, it's convenient to develop to YAML
and then convert to JSON right before uploading.

If you would like to contribute another language, please fork and open a PR.

## Example:
`yaml_to_json.py < cf.yaml > cf.cftemplate`

`aws cloudformation create --template-body file://cf.cftemplate`

## CloudFormation Functions
Some common CloudFormation functions are non-obvious in YAML. 
The following are quick conversions.

<table>
<tr>
<td>JSON </td>
<td>YAML </td>
</tr>
<tr>
<td>
"Fn::GetAtt":<br>
  [ "MyLoadBalancer",<br>
    "DNSName" ]
</td>
<td>
Fn::GetAtt:<br>
- MyLoadBalancer<br>
- DNSName
</td>
</tr>
<tr>
<td>
"Fn::Join":<br>
  [ "delimiter",<br>
    [ comma-delimited, list, <br>
      of, values ] ]
</td>
<td>
Fn:Join:<br>
- delimiter<br>
- - comma-delimited<br>
&nbsp; - list<br>
&nbsp; - of<br>
&nbsp; - values
</td>
</tr>
<tr>
<td>
"Fn::FindInMap:"<br>
  [ "EbsOptimizedMap",
    { "Ref": "InstanceType" },
    "Optimized" ]
</td>
<td>
Fn::FindInMap:<br>
&nbsp; - EbsOptimizedMap
&nbsp; - Ref: InstanceType
&nbsp; - Optimized
</td>
</tr>
</table>
