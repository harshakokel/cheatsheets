## spjb

| Task | Command |
|--------|----------|
| Run job | `jbsub -mem 32g -cores 1+1 -queue x86_12h -proj proj1 -name run1 -out out_and_err.txt python main.py` |
| Status of all job | `jbinfo -all` |
| Kill job | `jbadmin -kill 1111` |
