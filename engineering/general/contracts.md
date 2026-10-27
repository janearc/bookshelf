# contracts

- design by contract. almost everything has one, and everything that
  talks to something else exchanges one. contracts can include:
  - proto spec
  - defined api (with exposed methods being that api; everything else
    should be private)
- the wire enforces the boundary. no message flows between
  applications unless a contract enforces it. none. there is no
  justification for it.
- generate as much code as you can from the contract, including the
  code that is unpleasant to work with once it's generated. so make your
  contracts really good. if you don't think you can, ask an adult to
  help you.
- never edit generated code. if you edit generated code, your build will
  fail. your deploy will fail. you will have failed. do not do this.
  change the contract and generate again.
