# p9 - Jenkins + GitHub webhook demo

Run tests locally: `pip install -r requirements.txt && pytest`

## Jenkins setup (localhost, Windows)
1. Install plugins: Git, GitHub, Pipeline, JUnit.
2. New Item -> Pipeline. Under "Build Triggers" tick **GitHub hook trigger for GITScm polling**.
3. Pipeline -> "Pipeline script from SCM" -> Git -> your repo URL, Script Path: `p9/Jenkinsfile`.
4. Make localhost reachable: `ngrok http 8080` (gives https://xxxx.ngrok-free.app).

## GitHub webhook
Repo -> Settings -> Webhooks -> Add webhook
- Payload URL: `https://xxxx.ngrok-free.app/github-webhook/` (trailing slash required)
- Content type: `application/json`
- Event: "Just the push event"

Every `git push` now triggers the pipeline.
