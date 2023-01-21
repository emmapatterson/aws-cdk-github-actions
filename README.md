# AWS-CDK GitHub Actions

AWS-CDK GitHub Actions allow you to run `cdk deploy` and `cdk diff` (among other cdk subcommands) on your pull requests to help you review.

## Supported language

- TypeScript
- JavaScript
- Python
- Golang

## Example usage

```yaml
on: [push]

jobs:
  aws_cdk:
    runs-on: ubuntu-latest
    steps:

      - name: cdk diff
        uses: emmapatterson/aws-cdk-github-actions@v1.0.0
        with:
          cdk_subcommand: 'diff'
          cdk_directory: 'cdk'
          actions_comment: true
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_DEFAULT_REGION: 'ap-northeast-1'

      - name: cdk deploy
        uses: emmapatterson/aws-cdk-github-actions@v1.0.0
        with:
          cdk_subcommand: 'deploy'
          cdk_stack: 'stack1'
          cdk_args: '--require-approval never'
          cdk_directory: 'cdk'
          actions_comment: false
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_DEFAULT_REGION: 'ap-northeast-1'

      - name: cdk synth
        uses: emmapatterson/aws-cdk-github-actions@v1.0.0
        with:
          cdk_subcommand: 'synth'
          cdk_version: '1.16.2'
          cdk_directory: 'cdk'
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_DEFAULT_REGION: 'ap-northeast-1'
```

## Inputs

- `cdk_subcommand` **Required** AWS CDK subcommand to execute ('deploy', 'diff', etc.)
- `cdk_version` AWS CDK version to install. (default: 'latest')
- `cdk_stack` AWS CDK stack name to execute. (default: '*')
- `cdk_directory` Where your CDK project lives. (default: '.')
- `actions_comment` Whether or not to comment on pull requests. (default: true)
- `debug_log` Enable debug-log. (default: false)

## Outputs

- `status_code` Returned status code.

## ENV

- `AWS_ACCESS_KEY_ID` **Required**
- `AWS_SECRET_ACCESS_KEY` **Required**
- `GITHUB_TOKEN` Required for `actions_comment=true`

Recommended to get `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` from secrets. The github token is [automatically made available](https://help.github.com/en/actions/configuring-and-managing-workflows/authenticating-with-the-github_token) as a secret as `GITHUB_TOKEN`. 

## License

[MIT](LICENSE)

## Author

[youyo](https://github.com/youyo)
