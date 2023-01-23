# CMS Tryouts

## Strapi
Well this is nice. Very nice. But how about user pricing? 
Even if selfhosted you have to pay for admin? no multiple roles?

## Ghost
Huh? Why would you use this?
I can only make posts? No nested routes? No custom content stuff.

## Directus
Epic, use this.


```yaml
name: refresh map

on:
  schedule:
    - cron: "30 11 * * *"    #runs at 11:30 UTC everyday

jobs:
  getdataandrefreshmap:
    runs-on: ubuntu-latest
    steps:
      - name: checkout repo content
        uses: actions/checkout@v3 # checkout the repository content to github runner.
      - name: setup python
        uses: actions/setup-python@v4
        with:
          python-version: 3.8 #install the python needed
      - name: Install dependencies
        run: |
          if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
      - name: execute py script
        run: |
          python main.py
          git config user.name github-actions
          git config user.email github-actions@github.com
          git add .
          git commit -m "crongenerated"
          git push
```