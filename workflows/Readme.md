<h1 align="center" id="title">How to set workflow</h1>

<p id="description">This is the instructions to help you setup github workflow</p>

<h2>🛠️ Installation Steps:</h2>

<p>1. make folder .github</p>

<p>2. add your workflow yml file in the folder</p>

<p>3. start writing yml</p>

<h2>🍰 Contribution Guidelines:</h2>

```name: Example workflow
on: push #wheneven someone push 

jobs: 
  run-script:
  #define which machine will run
    runs-on: ubuntu-latest
    steps:
      - name: echo a name
        run: echo "I am from Github Actions"
      - name: multiline script
        run: |-     #run multi line script
          echo "printing versions of npm and node"
          node -v
          npm -v
```

# written by Yulin Xia