# JFrog

{
    "auths": {
        "macazcol.jfrog.io": {
            "username": "macazzzzzzzzzz@gmail.com",
            "password": "cmVmdGtuOjAxOjE3MzMzMDg1MDc6bjZPb2FqNUJJSmo0d29vblVJc0dXYW0zTURn",
            "email": "macazzzzzzzzzz@gmail.com"
        }
    }
}

## jfrog credentials saved in Gitlab
ARTIFACTORY_USER   macazzzzzzzzzz@gmail.com 
ARTIFACTORY_URL     macazcol.jfrog.io
ARTIFACTORY_API_TOKEN  cmVmdGtuOjAxOjE3MzMzMDg1MDc6bjZPb2FqNUJJSmo0d29vblVJc0dXYW0zTURn

**NOTE:** I have a local repo already in jfrog called:  docker-trial
**NOTE:** Heres how my image was saved: [*** macazcol.jfrog.io/docker-trial/networking:main-1104829054 | macazcol.jfrog.io/docker-trial/cafanwii/networking:main-23-12-1104843216-v1.0.0 ***]
**heres the config i used for my gitlab-runner**

```yml
apiVersion: v1
kind: ConfigMap
metadata:
  name: gitlab-runner-config-group
  namespace: gitlab-runner
data:
  config.toml: |-
    concurrent = 30

    [[runners]]
      name = "sosotech-group-runner"
      url = "https://gitlab.com/"
      id = 30312091
      token = "glrt-mQsuZKjvySuc47sWbj7D"
      token_obtained_at = 2023-12-10T00:52:28Z
      token_expires_at = 0001-01-01T00:00:00Z
      executor = "kubernetes"
      [runners.cache]
        MaxUploadedArchiveSize = 0

      [runners.kubernetes]
        namespace = "gitlab-runner"
        poll_timeout = 600
        cpu_request = "1"
        cpu_limit = "2" 
        memory_request = "256Mi"  
        memory_limit = "512Mi"  
        service_cpu_request = "200m"
        service_cpu_limit = "400m"  
        tags = ["cafanwii-group-runner"] 
        image = "docker:latest"
        helper-image = "alpine:latest"
        helper_cpu_limit = "2500m"
        helper_cpu_request = "41m"
        helper_memory_limit = "800Mi"
        helper_memory_request = "74Mi"
        [runners.kubernetes.volumes]
          [[runners.kubernetes.volumes.host_path]]
            name = "docker-socket"
            mount_path = "/var/run/docker.sock"
            read_only = true
```