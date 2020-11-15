# Ngrok tunelling Github Action

This is a Github Action that can be used in your Github Workflow to tunnel incoming/outgoing TCP traffic in your workflow environment.

The original use case for this was to achieve temporary deployment for CTF challenges under development but it can be as well used in many more other cases. 

## How to use this Action

This action accepts the following parameters

| Name| Description | Required  | Default |
| ------------- |-------------|-----|-----|
| timeout | After this timeout the deployment will automatically shutdown the tunelling and therefore stop the action. (max is 6 hours) | No | 1h |
| port | The port in localhost to forward traffic from/to  | Yes | - |
| ngrok_authtoken | Your ngrok authtoken| Yes | - |

Here is an example of using this action:

```yaml
name: CI
on: push

jobs:

  deploy:
    name: Deploy challenge
    runs-on: ubuntu-latest
    needs: cancel

    steps:
    - name: Checkout
      uses: actions/checkout@v2
    
    - name: Run container
      run: docker-compose up -d 
    
    - uses: apogiatzis/ngrok-tunneling-action@<VERSION>
      with:
        timeout: 1h
        port: 4000
        ngrok_authtoken: ${{ secrets.NGROK_AUTHTOKEN }}
```