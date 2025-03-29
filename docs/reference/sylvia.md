# Sylvia

**Sylvia** is a **symbolic execution engine** built to handle Verilog RTL directly.
It uses a strategy called **piecewise composition** to reduce the path-explosion 
problem commonly seen in symbolic execution.

- **Cycle-Accurate**: It interprets hardware designs with clock-cycle precision.
- **Scalable**: By splitting logic into independent blocks, it minimizes redundant work.

In **Veriviz**, Sylvia receives requests from SEIF, performs the necessary symbolic
analysis, and returns the results to the Veriviz backend, which then forwards them
to the front end for visualization.


## Citation

@inproceedings{Ryan2023Sylvia, author = {Ryan, Kaki and Sturton, Cynthia}, title = {Sylvia: Countering the Path Explosion Problem in the Symbolic Execution of Hardware Designs}, year = {2023}, isbn = {978-3-85448-060-0}, publisher = {TU Wien Academic Press}, address = {New York, NY, USA}, url = {https://repositum.tuwien.at/handle/20.500.12708/188806 }, booktitle = {Proceedings of the 23rd Conference on Formal Methods in Computer-Aided Design (FMCAD)}, pages = {110--121}, numpages = {12}, series = {FMCAD} }