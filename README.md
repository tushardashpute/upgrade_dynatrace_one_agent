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
