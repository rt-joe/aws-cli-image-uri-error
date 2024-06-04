# aws sam cli image uri error

Reproduces aws sam cli issue https://github.com/aws/aws-sam-cli/issues/7117

## steps

1. install aws sam cli `v1.117.0`
2. configure aws credentials
3. run `sam deploy`

## example debug output

```
2024-06-04 23:25:16,343 | No config file found in this directory.                                                                                                        
2024-06-04 23:25:16,345 | OSError occurred while reading TOML file: [Errno 2] No such file or directory: '<redacted>/aws-cli-image-uri-error/samconfig.toml'
2024-06-04 23:25:16,345 | Config file location: <redacted>/aws-cli-image-uri-error/samconfig.toml                                                           
2024-06-04 23:25:16,346 | Config file '<redacted>/aws-cli-image-uri-error/samconfig.toml' does not exist                                                    
2024-06-04 23:25:16,347 | Using SAM Template at <redacted>/aws-cli-image-uri-error/template.yml                                                             
2024-06-04 23:25:16,361 | OSError occurred while reading TOML file: [Errno 2] No such file or directory: '<redacted>/aws-cli-image-uri-error/samconfig.toml'
2024-06-04 23:25:16,363 | Using config file: samconfig.toml, config environment: default                                                                                 
2024-06-04 23:25:16,363 | Expand command line arguments to:                                                                                                              
2024-06-04 23:25:16,364 | --template_file=<redacted>/aws-cli-image-uri-error/template.yml --stack_name=aws-cli-image-uri --resolve_image_repos              
--fail_on_empty_changeset --on_failure=ROLLBACK                                                                                                                          
2024-06-04 23:25:17,009 | Collected default values for parameters: {'LambdaImageRepoUri': 'public.ecr.aws/lambda/nodejs'}                                                
2024-06-04 23:25:17,038 | There is no customer defined id or cdk path defined for resource ExampleLambda, so we will use the resource logical id as the resource id      
2024-06-04 23:25:17,039 | Unable to resolve property imageTag: {'Fn::FindInMap': ['TagLookup', 'Key', 'Tag']}. Leaving as is.                                            
2024-06-04 23:25:17,040 | Unable to resolve property ImageUri: {'Fn::Sub': ['${LambdaImageRepoUri}:${imageTag}', OrderedDict([('imageTag', {'Fn::FindInMap':             
['TagLookup', 'Key', 'Tag']})])]}. Leaving as is.                                                                                                                        
2024-06-04 23:25:17,041 | 0 stacks found in the template                                                                                                                 
2024-06-04 23:25:17,041 | Collected default values for parameters: {'LambdaImageRepoUri': 'public.ecr.aws/lambda/nodejs'}                                                
2024-06-04 23:25:17,055 | There is no customer defined id or cdk path defined for resource ExampleLambda, so we will use the resource logical id as the resource id      
2024-06-04 23:25:17,056 | Unable to resolve property imageTag: {'Fn::FindInMap': ['TagLookup', 'Key', 'Tag']}. Leaving as is.                                            
2024-06-04 23:25:17,057 | Unable to resolve property ImageUri: {'Fn::Sub': ['${LambdaImageRepoUri}:${imageTag}', OrderedDict([('imageTag', {'Fn::FindInMap':             
['TagLookup', 'Key', 'Tag']})])]}. Leaving as is.                                                                                                                        
2024-06-04 23:25:17,057 | 1 resources found in the stack                                                                                                                 
2024-06-04 23:25:17,058 | Found Serverless function with name='ExampleLambda' and ImageUri='{'Fn::Sub': ['${LambdaImageRepoUri}:${imageTag}', OrderedDict([('imageTag',  
{'Fn::FindInMap': ['TagLookup', 'Key', 'Tag']})])]}'                                                                                                                     
2024-06-04 23:25:17,058 | --base-dir is not presented, adjusting uri . relative to <redacted>/aws-cli-image-uri-error/template.yml                          
2024-06-04 23:25:17,059 | Telemetry endpoint configured to be https://aws-serverless-tools-telemetry.us-west-2.amazonaws.com/metrics                                     
2024-06-04 23:25:17,090 | Telemetry endpoint configured to be https://aws-serverless-tools-telemetry.us-west-2.amazonaws.com/metrics                                     
2024-06-04 23:25:17,091 | Sending Telemetry: {'metrics': [{'commandRun': {'requestId': 'd1c48943-5afd-456f-a017-e046a8549c5e', 'installationId':                         
'781031a4-ebae-4722-bc16-0af351578ec4', 'sessionId': '32e6f7ae-7597-4ca5-923f-5fd41fcc0a5d', 'executionEnvironment': 'CLI', 'ci': False, 'pyversion': '3.8.13',          
'samcliVersion': '1.117.0', 'awsProfileProvided': False, 'debugFlagProvided': True, 'region': '', 'commandName': 'sam deploy', 'metricSpecificAttributes':               
{'projectType': 'CFN', 'gitOrigin': None, 'projectName': '2d07c044ef8055ae129b04ccf56b9a9558b020a55b6e778d5c8796bb2e563398', 'initialCommit': None}, 'duration': 696,    
'exitReason': 'TypeError', 'exitCode': 255}}]}                                                                                                                           
2024-06-04 23:25:17,091 | Unable to find Click Context for getting session_id.                                                                                           
2024-06-04 23:25:17,095 | Sending Telemetry: {'metrics': [{'events': {'requestId': 'c18fe795-f893-42bb-9649-f8418795a927', 'installationId':                             
'781031a4-ebae-4722-bc16-0af351578ec4', 'sessionId': '32e6f7ae-7597-4ca5-923f-5fd41fcc0a5d', 'executionEnvironment': 'CLI', 'ci': False, 'pyversion': '3.8.13',          
'samcliVersion': '1.117.0', 'commandName': 'sam deploy', 'metricSpecificAttributes': {'events': [{'event_name': 'SamConfigFileExtension', 'event_value': '.toml',        
'thread_id': 'b71752b7835842b3a0fc7efd61fbef7a', 'time_stamp': '2024-06-04 21:25:16.345', 'exception_name': None}, {'event_name': 'SamConfigFileExtension',              
'event_value': '.toml', 'thread_id': '85c42d180399480bbdd39a2c891953e3', 'time_stamp': '2024-06-04 21:25:16.362', 'exception_name': None}]}}}]}                          
2024-06-04 23:25:17,573 | HTTPSConnectionPool(host='aws-serverless-tools-telemetry.us-west-2.amazonaws.com', port=443): Read timed out. (read timeout=0.1)               
2024-06-04 23:25:17,578 | HTTPSConnectionPool(host='aws-serverless-tools-telemetry.us-west-2.amazonaws.com', port=443): Read timed out. (read timeout=0.1)               

Error: expected str, bytes or os.PathLike object, not dict
Traceback:
  File "click/core.py", line 1078, in main
  File "click/core.py", line 1688, in invoke
  File "click/core.py", line 1434, in invoke
  File "click/core.py", line 783, in invoke
  File "samcli/cli/cli_config_file.py", line 347, in wrapper
  File "samcli/lib/cli_validation/image_repository_validation.py", line 111, in wrapped
  File "click/decorators.py", line 92, in new_func
  File "click/core.py", line 783, in invoke
  File "samcli/lib/telemetry/metric.py", line 185, in wrapped
  File "samcli/lib/telemetry/metric.py", line 150, in wrapped
  File "samcli/lib/utils/version_checker.py", line 43, in wrapped
  File "samcli/cli/main.py", line 95, in wrapper
  File "samcli/commands/_utils/cdk_support_decorators.py", line 40, in wrapped
  File "samcli/commands/_utils/command_exception_handler.py", line 89, in wrapper_command_exception_handler
  File "samcli/commands/_utils/command_exception_handler.py", line 69, in wrapper_command_exception_handler
  File "samcli/commands/deploy/command.py", line 201, in cli
  File "samcli/commands/deploy/command.py", line 308, in do_cli
  File "samcli/lib/bootstrap/companion_stack/companion_stack_manager.py", line 311, in sync_ecr_stack
  File "samcli/lib/providers/sam_function_provider.py", line 71, in __init__
  File "samcli/lib/providers/sam_function_provider.py", line 246, in _extract_functions
  File "samcli/lib/providers/sam_function_provider.py", line 315, in _convert_sam_function_resource
  File "samcli/lib/providers/sam_function_provider.py", line 451, in _build_function_configuration
  File "samcli/lib/providers/sam_stack_provider.py", line 379, in normalize_resource_path
  File "posixpath.py", line 62, in isabs

An unexpected error was encountered while executing "sam deploy".
Search for an existing issue:
https://github.com/aws/aws-sam-cli/issues?q=is%3Aissue+is%3Aopen+Bug%3A%20sam%20deploy%20-%20TypeError
Or create a bug report:
https://github.com/aws/aws-sam-cli/issues/new?template=Bug_report.md&title=Bug%3A%20sam%20deploy%20-%20TypeError
```