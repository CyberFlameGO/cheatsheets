# ezjail

> Jail management made bearable.

## Table of Contents

* [Set CPU Affinity](#set-cpu-affinity)

### Set CPU Affinity
You can limit the specific cores a jail uses but not a number of automatically scheduled ones. This can be done as a single core, a range of cores or a list cores.
```
ezjail-admin config -c <CORE_NUMBER> <JAIL_NAME>
```
Where `<CORE_NUMBER>` is the core number you want your jail on, with `0` being the first and `n-1` being the last should you have `n` cores, and `<JAIL_NAME>` being the name of the ezjail-managed jail you want to set the affinity of.

```
ezjail-admin config -c <CORE_NUMBER_FIRST>-<CORE_NUMBER_LAST> <JAIL_NAME>
```
Where `<CORE_NUMBER_FIRST>` and `<CORE_NUMBER_LAST>` are the first and last cores you want to run on respectively, and `<JAIL_NAME>` being the jail name.

```
ezjail-admin config -c <CORE_NUMBER_FIRST>,<CORE_NUMBER_SECOND>,...,<CORE_NUMBER_N> <JAIL_NAME>
```

Where core numbers like `<CORE_NUMBER_FIRST>`, `<CORE_NUMBER_LAST>`, and `<CORE_NUMBER_N>` are the core numbers you want to run on, and `<JAIL_NAME>` being the jail name.
