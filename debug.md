## Summary of Issues

1. Error with Contexts:
<img width="2199" height="1226" alt="image" src="https://github.com/user-attachments/assets/a89e8b5c-e37b-4827-b6de-8581ccc004b8" />
<img width="1802" height="1289" alt="image" src="https://github.com/user-attachments/assets/049c6972-772f-411b-839d-c801e45e796e" />

- Attempted to use GenAI "Explain the error" feature, got loading icon of death for a min or so
  <img width="708" height="1362" alt="image" src="https://github.com/user-attachments/assets/d113f6ee-8b65-4af3-a19a-855ad93e7d48" />
- Provided explanation was too generic and vaguely mentioned every case that could go wrong,
  i.e, incorrect source code, mishandled edge cases, issue with env, typographical errors, and datatype mismatches.
  <img width="622" height="1299" alt="image" src="https://github.com/user-attachments/assets/e109969d-aad5-429d-a089-d166d7ac9154" />
  <img width="624" height="1363" alt="image" src="https://github.com/user-attachments/assets/6875100c-55df-40e4-85bc-8018590ac68a" />
Manual Debugging:
- We see that grep returned exit status 1, what cases would that happen in?
- Probably a bad setup. We know reality check looks for the env vars under the global and individual-local contexts
- If grep returns exit status 1, the job can't find the env var under the global context
- Steps taken:
-   Check case and naming to make sure it matches the yaml EXACTLY (org-global, CONTEXT_END_TO_END_TEST_VAR)
-   Check the security permissions(set to all members)
<img width="1985" height="672" alt="image" src="https://github.com/user-attachments/assets/76ba0c85-8889-4b1e-840b-afd1b80dbcf6" />

-   Since Everything seems fine, add some logs to the yaml
   ``` run:
    name: Debug env injection
    command: |
      echo "Dumping all env vars for troubleshooting:"
      env | sort
      echo "Now grepping for the test var:"
      env | grep CONTEXT_END_TO_END_TEST_VAR
  ```

Issue:
<img width="2179" height="718" alt="image" src="https://github.com/user-attachments/assets/2ee7976f-ef6e-4193-8575-869d3162fa35" />

- Tried using CircleCI's AI editor to "auto fix" the issue.
  <img width="1790" height="729" alt="image" src="https://github.com/user-attachments/assets/6bf7d698-42fd-44ab-b9f8-7822ef80953b" />

- Manually fixed an indentation issue I found, clicked on save and run. After a *long* loading periond, got this-
  <img width="753" height="901" alt="image" src="https://github.com/user-attachments/assets/f25db3c5-c94c-4aff-8c55-f3650b7efc35" />

Updated raw config.yaml on Github and pushed, issue resolved
<img width="2204" height="1215" alt="image" src="https://github.com/user-attachments/assets/63032e7b-5d72-4894-955c-9f4cb8adb8d8" />
<img width="1641" height="1212" alt="image" src="https://github.com/user-attachments/assets/8d303872-0100-4e0b-816a-812d18a865a0" />




