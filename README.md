# upgrade_dynatrace_one_agent

To update Dynatrace Operator, select one of the following, depending on your deployment type.

For cloudNativeFullStack, applicationMonitoring with CSI driver, and hostMonitoring when readonly isn't disabled, run the commands below.

      kubectl apply -f https://github.com/Dynatrace/dynatrace-operator/releases/download/v0.10.2/kubernetes.yaml
      kubectl apply -f https://github.com/Dynatrace/dynatrace-operator/releases/download/v0.10.2/kubernetes-csi.yaml
      
Update OneAgent if automatic updates are disabled

By default, Dynatrace Operator handles OneAgent updates automatically. If you choose to disable automatic updates, and haven't set any standard OneAgent version in Dynatrace, you can manually update OneAgent by running the command below.

      kubectl -n dynatrace rollout restart daemonset/<DYNAKUBE>-oneagent

Updating tokens
If you need to update your tokens, follow the steps below.

1. Find current tokens

Find and save your currently used tokens.

Note: After generating new tokens, you'll need to delete the old ones.
      
      kubectl -n dynatrace get secrets <dynakube-name> -o yaml | yq '.data.apiToken' | base64 -d
      
2. Delete your secret
      
      kubectl -n dynatrace delete secret dynakube
      
3. Create new tokens

For instructions on how to create the tokens, see Tokens and permissions required. --> https://www.dynatrace.com/support/help/setup-and-configuration/setup-on-container-platforms/kubernetes/get-started-with-kubernetes-monitoring#tokens

copy the new token generated.

4. Create a new secret with updated tokens

To create a new secret with the updated tokens, run one of the commands below, making sure to replace the placeholders with the new tokens.

      kubectl -n dynatrace create secret generic dynakube --from-literal="apiToken=<API-TOKEN>"
      
      kubectl -n dynatrace create secret generic dynakube --from-literal="apiToken=<API-TOKEN>" --from-literal="dataIngestToken=<INGEST-TOKEN>"
      
Dynatrace Operator picks up the updated secrets in approximately five minutes. Removing DynaKube and reapplying it forces an instant reconciliation.

5. Delete the old token

After the new tokens are in place, delete the old ones.

In Dynatrace, 
      go to Access tokens and look for the old token.
      Select Delete.
      
**Set up Kubernetes/OpenShift monitoring with Helm**

