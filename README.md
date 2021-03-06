# Shiny-Potato

This small tool can be used to deploy several alpine pods
with a persistent volume attached to it. This can be used
to detect problems when binding pvc to pods.

Regarding the name, I just took the first name GitHub proposed me :smile:

## Build

```
go build
```

## Usage

By default, it will write the json results into `shiny-potato.json`

`kubeconfig` can be set using the env var `KUBECONFIG`

```
You must pass a sub-command: [deploy|clean]

  -count int
    	Number of pod with pvc to create (default 3)
  -image string
    	pod image (default "docker.io/alpine:latest")
  -kubeconfig string
    	absolute path to the kubeconfig file (mandatory)
  -namespace string
    	namespace for the pods (default "default")
  -no-results
    	do not output json results at all
  -no-results-file
    	do not write the json results to a file
  -prefix string
    	name prefix used for pods and pvcs (default "shiny-potato")
  -pvc-size string
    	Requested size of the PersistentVolumeClaims (default "100m")
  -results-file string
    	path to write the json results (default "shiny-potato.json")
  -results-stdout
    	show json results to stdout (verbose)
  -storage-class string
    	Storage Class of the PersistentVolumeClaims (mandatory)
```

## Sub-commands

**deploy**

```console
shiny-potato deploy -storage-class csi-cephfs-sc
>>> Starting: 2020-06-04 10:59:20.585475331 +0200 CEST m=+0.020491001
>>> [POD] default/shiny-potato-0001 creating...
>>> [PVCLAIM] default/shiny-potato-0001 creating...
>>> [PVCLAIM] default/shiny-potato-0001 created
>>> [PVCLAIM] default/shiny-potato-0001 waiting to be bound....
>>> [POD] default/shiny-potato-0001 created
>>> [POD] default/shiny-potato-0001 waiting to be ready....
>>> [POD] default/shiny-potato-0002 creating...
>>> [PVCLAIM] default/shiny-potato-0002 creating...
>>> [POD] default/shiny-potato-0003 creating...
>>> [PVCLAIM] default/shiny-potato-0003 creating...
>>> [PVCLAIM] default/shiny-potato-0002 created
>>> [PVCLAIM] default/shiny-potato-0002 waiting to be bound....
>>> [POD] default/shiny-potato-0002 created
>>> [POD] default/shiny-potato-0002 waiting to be ready....
>>> [PVCLAIM] default/shiny-potato-0003 created
>>> [PVCLAIM] default/shiny-potato-0003 waiting to be bound....
>>> [POD] default/shiny-potato-0003 created
>>> [POD] default/shiny-potato-0003 waiting to be ready....
>>> [PVCLAIM] default/shiny-potato-0001 waiting to be bound....
>>> [POD] default/shiny-potato-0001 waiting to be ready....
>>> [PVCLAIM] default/shiny-potato-0001 bound, time elapsed: 6.153821531s
>>> [PVCLAIM] default/shiny-potato-0002 waiting to be bound....
>>> [POD] default/shiny-potato-0002 waiting to be ready....
>>> [PVCLAIM] default/shiny-potato-0003 waiting to be bound....
>>> [POD] default/shiny-potato-0003 waiting to be ready....
>>> [PVCLAIM] default/shiny-potato-0002 bound, time elapsed: 5.571097944s
>>> [PVCLAIM] default/shiny-potato-0003 bound, time elapsed: 5.567823008s
>>> [POD] default/shiny-potato-0001 waiting to be ready....
>>> [POD] default/shiny-potato-0001 ready, time elapsed: 11.170447256s
>>> [POD] default/shiny-potato-0002 waiting to be ready....
>>> [POD] default/shiny-potato-0003 waiting to be ready....
>>> [POD] default/shiny-potato-0002 waiting to be ready....
>>> [POD] default/shiny-potato-0003 waiting to be ready....
>>> [POD] default/shiny-potato-0002 waiting to be ready....
>>> [POD] default/shiny-potato-0003 waiting to be ready....
>>> [POD] default/shiny-potato-0002 ready, time elapsed: 20.57174206s
>>> [POD] default/shiny-potato-0003 waiting to be ready....
>>> [POD] default/shiny-potato-0003 ready, time elapsed: 25.691817578s
>>> Writing results to: shiny-potato.json
>>> Results successfully written to file
>>> Finished: 2020-06-04 10:59:48.418761508 +0200 CEST m=+27.853776909
>>> Duration: 27.833307273s
```

**clean**

```console
shiny-potato clean -storage-class csi-cephfs-sc
>>> Starting: 2020-06-04 11:00:52.864378028 +0200 CEST m=+0.017911112
>>> [POD] default/shiny-potato-0001 deleting...
>>> [PVCLAIM] default/shiny-potato-0001 deleting...
>>> [PVCLAIM] default/shiny-potato-0001 deletion started
>>> [PVCLAIM] default/shiny-potato-0001 waiting to be deleted...
>>> [POD] default/shiny-potato-0001 deleting started
>>> [POD] default/shiny-potato-0001 waiting to be deleted....
>>> [POD] default/shiny-potato-0002 deleting...
>>> [PVCLAIM] default/shiny-potato-0002 deleting...
>>> [POD] default/shiny-potato-0003 deleting...
>>> [PVCLAIM] default/shiny-potato-0003 deleting...
>>> [PVCLAIM] default/shiny-potato-0002 deletion started
>>> [PVCLAIM] default/shiny-potato-0002 waiting to be deleted...
>>> [POD] default/shiny-potato-0002 deleting started
>>> [POD] default/shiny-potato-0002 waiting to be deleted....
>>> [PVCLAIM] default/shiny-potato-0003 deletion started
>>> [PVCLAIM] default/shiny-potato-0003 waiting to be deleted...
>>> [POD] default/shiny-potato-0003 deleting started
>>> [POD] default/shiny-potato-0003 waiting to be deleted....
>>> [PVCLAIM] default/shiny-potato-0001 waiting to be deleted...
>>> [POD] default/shiny-potato-0001 waiting to be deleted....
>>> [PVCLAIM] default/shiny-potato-0002 waiting to be deleted...
>>> [POD] default/shiny-potato-0002 waiting to be deleted....
>>> [PVCLAIM] default/shiny-potato-0001 waiting to be deleted...
[...]
>>> [POD] default/shiny-potato-0001 waiting to be deleted....
>>> [PVCLAIM] default/shiny-potato-0001 deleted, time elapsed: 36.15215162s
>>> [POD] default/shiny-potato-0001 deleted, time elapsed: 36.161191617s
>>> [PVCLAIM] default/shiny-potato-0002 waiting to be deleted...
>>> [POD] default/shiny-potato-0002 waiting to be deleted....
>>> [PVCLAIM] default/shiny-potato-0003 waiting to be deleted...
>>> [POD] default/shiny-potato-0003 waiting to be deleted....
>>> [PVCLAIM] default/shiny-potato-0003 deleted, time elapsed: 35.689291456s
>>> [POD] default/shiny-potato-0003 deleted, time elapsed: 35.689914716s
>>> [PVCLAIM] default/shiny-potato-0002 waiting to be deleted...
>>> [POD] default/shiny-potato-0002 waiting to be deleted....
>>> [PVCLAIM] default/shiny-potato-0002 waiting to be deleted...
>>> [POD] default/shiny-potato-0002 waiting to be deleted....
>>> [PVCLAIM] default/shiny-potato-0002 deleted, time elapsed: 45.570578343s
>>> [POD] default/shiny-potato-0002 deleted, time elapsed: 45.571663517s
>>> Writing results to: shiny-potato.json
>>> Results successfully written to file
>>> Finished: 2020-06-04 11:01:40.518268628 +0200 CEST m=+47.671801692
>>> Duration: 47.653914475s
```


## json results

Depending of the command, the duration represents:
* For a PVC, the time from creation to the `Bound` state
* For a POD, the time from creation to the `Ready` state

There is 4s max (default poll interval) margin.

```json
{
  "Namespace": "default",
  "Command": "deploy",
  "Pvc": [
    {
      "Name": "shiny-potato-0001",
      "Size": "100m",
      "StorageClass": "csi-cephfs-sc",
      "Timings": {
        "Start": "2020-06-04T10:59:20.586228542+02:00",
        "End": "2020-06-04T10:59:26.740048845+02:00",
        "Duration": "6.153821531s"
      }
    },
    {
      "Name": "shiny-potato-0002",
      "Size": "100m",
      "StorageClass": "csi-cephfs-sc",
      "Timings": {
        "Start": "2020-06-04T10:59:22.666996892+02:00",
        "End": "2020-06-04T10:59:28.238094578+02:00",
        "Duration": "5.571097944s"
      }
    },
    {
      "Name": "shiny-potato-0003",
      "Size": "100m",
      "StorageClass": "csi-cephfs-sc",
      "Timings": {
        "Start": "2020-06-04T10:59:22.726149348+02:00",
        "End": "2020-06-04T10:59:28.29397189+02:00",
        "Duration": "5.567823008s"
      }
    }
  ],
  "Pod": [
    {
      "Name": "shiny-potato-0001",
      "Timings": {
        "Start": "2020-06-04T10:59:20.58568825+02:00",
        "End": "2020-06-04T10:59:31.756135271+02:00",
        "Duration": "11.170447256s"
      }
    },
    {
      "Name": "shiny-potato-0002",
      "Timings": {
        "Start": "2020-06-04T10:59:22.666967151+02:00",
        "End": "2020-06-04T10:59:43.238709012+02:00",
        "Duration": "20.57174206s"
      }
    },
    {
      "Name": "shiny-potato-0003",
      "Timings": {
        "Start": "2020-06-04T10:59:22.726095152+02:00",
        "End": "2020-06-04T10:59:48.41791242+02:00",
        "Duration": "25.691817578s"
      }
    }
  ]
}
```
