1. Fork realitycheck repo from circleci to personal repo
2. Setup repository in circleci project settings:
  <img width="2788" height="1374" alt="image" src="https://github.com/user-attachments/assets/97cea4f9-3b46-431a-86d6-437d7392a820" />

3. Generate a personal api token
  <img width="1425" height="1037" alt="image" src="https://github.com/user-attachments/assets/6ebb39be-f885-4b81-9844-ffd834697c19" />
- copy token (you won't see it again)

4. Add Token to environment variables
  <img width="1513" height="1021" alt="image" src="https://github.com/user-attachments/assets/27cc7846-5fa9-43c1-940b-e4a6d4425e14" />
- This token is used by CircleCI jobs to verify resource classes, confirm workflows, and cancel incorrectly triggered jobs.
- The jobs make API calls to CircleCI (via curl or PowerShell) to fetch job details → they need an API token to authenticate.

5. Adding the CIRCLE_HOSTNAME url to environment variables:
- Most enterprise apps are self-hosted (https://app.server.example.com/dashboard/) and the trailing '/dashboard' and 'app' subdomain will need to be removed.
- We will use CircleCI Saas (free) and so, the hostname will be **https://circleci.com**
  <img width="1537" height="1028" alt="image" src="https://github.com/user-attachments/assets/1d677ed4-7cbb-462c-9286-3e05b7111474" />


6. Setup cloud provider in environment variables
- gcp, aws, or other
  <img width="1506" height="1029" alt="image" src="https://github.com/user-attachments/assets/1c99ae8c-1a90-4e2d-96ee-c1cb1bf7b31b" />

7. Optional CIRCLE_WINDOWS_EXECUTOR
- Runs a windows executor resource class workflow that spins up jobs using the Windows executor inside CircleCI
- Needs Windows support (server installs need a specified windos vm, cloud needs it enabled via circleci)
- If CIRCLE_WINDOWS_EXECUTOR=true but your CircleCI account doesn’t have Windows enabled, fail with “Resource class not available” or “Executor not supported”.
  
8. Configuring Contexts:
- CircleCI will inject all env vars from the context (org-global, local etc) into that job.
- An error is thrown if the contexts aren't injected properly. we test global and individual-local
- Go to org settings-> contexts
  <img width="993" height="799" alt="image" src="https://github.com/user-attachments/assets/69f7c7de-e28a-4ffc-a003-ad88b933fc03" />
- Create global and individual-local contexts
  <img width="1945" height="677" alt="image" src="https://github.com/user-attachments/assets/9fca6a79-27bc-46b8-a876-fcead46fdd17" />
- Reality check makes sure context injection works properly, the actual values don't matter so we set to 1
  <img width="2788" height="1374" alt="image" src="https://github.com/user-attachments/assets/0d484079-7d0d-4244-a860-46184fbd2c8c" />
  <img width="1388" height="1055" alt="image" src="https://github.com/user-attachments/assets/2c5def14-6a94-44e5-aed3-48fc764b695c" />
  
9. Trigger the build-> empty commit+push/use trigger button

10. Check job runs and artifacts
