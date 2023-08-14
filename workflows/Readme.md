<h1 align="center" id="title">How to set workflow</h1>

<p id="description">This is the instructions to help you setup github workflow</p>

<h2>🛠️ Installation Steps:</h2>

<p>1. make folder .github</p>

<p>2. add your workflow yml file in the folder</p>

<p>3. start writing yml</p>

<h2>🍰 Contribution Guidelines:</h2>

name:name: Example workflow
name:on: push #wheneven someone push 
name:
name:jobs: 
name:  run-script:
name:  #define which machine will run
name:    runs-on: ubuntu-latest
name:    steps:
name:      - name: echo a name
name:        run: echo "I am from Github Actions"
name:      - name: multiline script
name:        run: |-     #run multi line script
name:          echo "printing versions of npm and node"
name:          node -v
name:          npm -v

# written by Yulin Xia