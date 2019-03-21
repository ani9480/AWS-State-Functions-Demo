# AWS-State-Functions-Demo

PFA, the definitions of the step functions. There are 2 step functions I have made.

1.	This uses 2 state machine definitions they are attached in step_function_1

Lambda functions used are 

async_invoke-  https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions/async_invoke?tab=graph

sendSuccess – https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions/sendSuccess?tab=graph

sendFailure - https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions/sendFailure?tab=graph


Input to the step function is the json file below. We execute the outer_state_machine and that starts the asynchronous process

{
"async_action_arguments": {
"data": "string"
},
"other_data": 5
}

References for the first step function: 

https://medium.com/semantive/part-1-asynchronous-actions-within-aws-step-functions-without-servers-f58e030a0e8b
https://medium.com/semantive/part-2-asynchronous-actions-within-aws-step-functions-without-servers-e2ef26aa75d9





2.	This is an inbuilt Glue job within AWS. Definition is attached in step_function_2


Lambda functions used are 

JobStatusPol-SubmitJobFunction  - https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions/StepFunctionsSample-JobStatusPol-SubmitJobFunction-5SF33L1IB899?tab=graph

JobStatusPoll-CheckJobFunction - https://console.aws.amazon.com/lambda/home?region=us-east-1#/functions/StepFunctionsSample-JobStatusPoll-CheckJobFunction-T0UY7CA7K8KX?tab=graph


Input to this state machine is


{
  "input": {
    "jobName": "my-job",
    "jobDefinition": "arn:aws:batch:us-east-1:350853315364:job-definition/SampleJobDefinition-16289f8f3904556:1",
    "jobQueue": "arn:aws:batch:us-east-1:350853315364:job-queue/SampleJobQueue-1cfb6e232b83481",
    "wait_time": 60
  },
  "roleArn": "arn:aws:iam::350853315364:role/StepFunctionsSample-JobStatusP-StatesExecutionRole-1JZ6U08B5QVEF"
}


Now here As I was telling in the call, the blueprint created a batch job definition and queue for us to use. If you go to Sample Projects under State machine there will be Job Poller in it. That will create the lambda functions and the batch job definition and queue.
