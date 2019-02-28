# ecs-cron

This script integrates awscli and ecs-cli to take advantage of AWS ECS scheduled task (cron).

> Inspired from [ecs-deploy](https://github.com/silinternational/ecs-deploy)

## Installation

* Install and configure [aws-cli](https://docs.aws.amazon.com/en_us/cli/latest/userguide/cli-chap-install.html)
* Install [ecs-cli](https://docs.aws.amazon.com/zh_tw/AmazonECS/latest/developerguide/ECS_CLI_installation.html)
* Install ecs-cron
```
curl https://raw.githubusercontent.com/ken8203/ecs-cron/master/ecs-cron | sudo tee /usr/local/bin/ecs-cron
sudo chmod +x /usr/local/bin/ecs-cron
```

## Usage

```
Required arguments:
    -c | --cluster               AWS ECS cluster name
    -t | --task-name             AWS ECS task definition name
    -e | --events-rule-name      AWS CloudWatch events rule name

Optional arguments:
    -r | --region                AWS region. Default is ap-northeast-1.
    -p | --profile               AWS profile. Default is default.
    -C | --compose-file          Path of docker-compose.yml. Default is ./docker-compose.yml
    -E | --ecs-params            Path of ecs-params.yml. Default is ./ecs-params.yml

Examples:
    Create a cron:
      ecs-cron up -c cluster_name -t task_name -e events_rule_name [ -r region ] [ -p profile ] [ -C docker-compose.yml ] [ -E ecs-params.yml ]

    Delete a cron:
      ecs-cron down -c cluster_name -t task_name -e events_rule_name [ -r region ] [ -p profile ]

Notes:
    Need docker-compose.yml and ecs-params.yml.
```

## Troubleshooting
1.  You must provide AWS credentials. Or you might see something like this:

    ```
    You must specify a region. You can also configure your region by running "aws configure".
    ```
2. If there is no existed CloudWatch events rule, you will see something like this:

    ```
    An error occurred (ResourceNotFoundException) when calling the PutTargets operation: Rule XXX does not exist.
    ```

## TODO
- [ ] Support key and secret parameters
- [ ] Support creating CloudWatch events rule
- [ ] Testing
