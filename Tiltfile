# Test case for https://github.com/tilt-dev/tilt-extensions/issues/92
#
# With the previous version of the Restart Process extension,
# this job (which will always fail) showed up green in the Tilt sidebar
# because we weren't correctly surfacing the exit code.
# See old behavior: https://cloud.tilt.dev/snapshot/AZS-w_gL231s6CjvZsA=
#
# With the latest change to Restart Process, this job should
# correctly show up RED on the sidebar.
# See current behavior: https://cloud.tilt.dev/snapshot/AfTmw_gL772d93lJMto=
#
# Note: you'll have to `rm -rf tilt_modules/restart_process` to let
# Tilt fetch the updated version of the extension.

load('ext://restart_process', 'docker_build_with_restart')

k8s_yaml('job.yaml')
docker_build_with_restart('failing_job', '.', '/fail.sh',
                          live_update=[sync('./fail.sh', '/fail.sh')])
