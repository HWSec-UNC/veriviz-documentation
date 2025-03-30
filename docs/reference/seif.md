# SEIF

---

**SEIF** (Symbolic Execution for Information Flow) is a tool that focuses on verifying
and exploring how information flows through hardware designs:

Read the paper [here](https://dl.acm.org/doi/10.1145/3623652.3623666)
- It **augments** symbolic execution to account for data and control signals, ensuring
  you can analyze potential leaks or unauthorized flows.
- SEIF integrates with **Sylvia** to refine the exploration of flows and generate
  more precise results.

In **Veriviz**, SEIF is called from the backend to run advanced security checks.
You can view or visualize the results via the Veriviz front end.

---

## Citation

@inproceedings{ryan2023SEIF,
  author    = {Ryan, Kaki and Gregoire, Matthew and Sturton, Cynthia},
  title     = {{SEIF: Augmented} Symbolic Execution for Information Flow in Hardware Designs},
  year      = {2023},
  isbn      = {9798400716232},
  publisher = {Association for Computing Machinery},
  address   = {New York, NY, USA},
  url       = {https://doi.org/10.1145/3623652.3623666},
  doi       = {10.1145/3623652.3623666},
  booktitle = {Proceedings of the 12th International Workshop on Hardware and Architectural Support for Security and Privacy (HASP)},
  pages     = {1--9},
  numpages  = {9},
  keywords  = {path coverage, information flow, symbolic execution, hardware security},
  location  = {Toronto, Canada},
}

