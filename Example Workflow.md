Below is an example Github workflow you could modify to grab rules and translate them daily.

```yml
name: Transform Sigma Windows Process Creation Events to KQL

on:
  schedule:
    - cron: '0 0 * * *'  # Run once per day at midnight

jobs:
  run-python-script:
    runs-on: self-hosted  # Change this value to 'ubuntu-latest' if you want to host it on Github.
    
    steps:
      - name: Checkout code
        uses: actions/checkout@v4.1.1
        
      - name: Set up Python
        uses: actions/setup-python@v4.7.1
        with:
          python-version: '3.10'
        
      - name: get sigma-cli # other parts of my CI/CD workflow use the sigma-cli - I've left it in, but you should be ok to remove this section and the plugin install steps too.
        run: |
          python -m pip install sigma-cli 
      
      - name: Install sigma-cli pipelines
        run: |
          sigma plugin install microsoft365defender
        
      - name: Get Sigma repository
        run: |
          git clone https://github.com/SigmaHQ/sigma.git
      
      - name: Run Sigma Windows process event creation script
        run: python sig_convert_win_process_create_markdown.py

      - name: Commit and push translated process creation rules
        run: |
          cd 'KQL - Windows Process Creation'
          git add $(find . -type f -name '*.md')
          git commit -m "New Rules Added" || true
          git push
          cd ..
```