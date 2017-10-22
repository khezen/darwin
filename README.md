[![GoDoc](https://img.shields.io/badge/go-documentation-blue.svg?style=flat-square)](https://godoc.org/github.com/khezen/darwin)
[![Build Status](http://img.shields.io/travis/khezen/darwin.svg?style=flat-square)](https://travis-ci.org/khezen/darwin) [![codecov](https://img.shields.io/codecov/c/github/khezen/darwin/master.svg?style=flat-square)](https://codecov.io/gh/khezen/darwin)
[![Go Report Card](https://goreportcard.com/badge/github.com/khezen/darwin?style=flat-square)](https://goreportcard.com/report/github.com/khezen/darwin)

# *darwin*
Genetic Algorithm written in Go
```golang
import "github.com/khezen/darwin"
```

```golang
type Individual interface {
	Fitness() float64
	SetFitness(float64)
}
```

```golang
type Population interface {
	sort.Interface
	Sort()
    	Max() Individual
	Min() Individual
	Extremums() (Individual, Individual)

    	Add(...Individual)
   	RemoveAt(int) error
	Remove(...Individual)
	Replace(int, Individual) error
    	Get(int) (Individual, error)
    	PickCouple() (index1 int, indiv1 Individual, index2 int, indiv2 Individual, err error)
	Has(...Individual) bool
	IndexOf(Individual) (int, error)

	Cap() int
	SetCap(int) error
	Truncate(int) error
}

```

```golang
type Evaluater interface {
	Evaluate(Individual) (Fitness float64)
}
```

```golang
type Selecter interface {
	Select(pop Population, survivorsSize int) (Population, error)
}
```

```golang
type Crosser interface {
	Cross(individual1, individual2 Individual) Individual
}
```

```golang
type Mutater interface {
	Mutate(Individual) Individual
}
```

```golang

type Lifecycle interface {
	Generation(pop Population, survivorSizeForSelection int, mutationProbability float64) (Population, error)
}

func New(s Selecter, c Crosser, m Mutater, e Evaluater) Lifecycle

```
