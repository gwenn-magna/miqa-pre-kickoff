# miqa-pre-kickoff
Returns information needed for Miqa trigger kickoff from GHA, when GHA kickoff is not an option.

This Action enables you to create a Check Run for your pull request so that a subsequent call to Miqa (i.e. from an outside script) has a destination to write results to. It does not call Miqa/trigger any executions.  If you run this action and then do _not_ make a corresponding call to Miqa with the outputs, you will have a Check Run on your pull request that is left in Pending status.


To use this action, call it in a step with a defined ID, and then pull the "CHECK_RUN_ID" output in a subsequent step where that information is needed.

```
- id: miqa-pre-kickoff
  uses: magna-labs/miqa-pre-kickoff@v1.0.0
  with:
    INSTALLATION_ID: 1234567
    CHECK_NAME: Miqa Test - d51a5677 - (${{ github.event_name }})
    GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    SHA: ${{ github.sha }}
    REPOSITORY: ${{ github.repository }}
- id: print_check_run_id
  name: Print check run ID
  shell: bash
  run: |
    echo "${{ steps.miqa-pre-kickoff.outputs.CHECK_RUN_ID }}"
```
