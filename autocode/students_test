package coverage

import (
	"fmt"
	"os"
	"testing"
	"time"

	"github.com/stretchr/testify/assert"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func errorExpectedValue(e interface{}, g interface{}) string {
	return fmt.Sprintf("Expected %v, but got %v", e, g)
}

func errorUnexpected(e interface{}) string {
	return fmt.Sprintf("Unexpected error: %v", e)
}

var husband Person = Person{"John", "Doe", time.Date(1970, time.January, 1, 1, 1, 0, 0, time.Local)}
var wife Person = Person{"Jane", "Doe", time.Date(1973, time.March, 3, 3, 3, 0, 0, time.Local)}
var twin01 Person = Person{"Ann", "Doe", time.Date(2000, time.March, 5, 5, 10, 0, 0, time.Local)}
var twin02 Person = Person{"Bob", "Doe", time.Date(2000, time.March, 5, 5, 10, 0, 0, time.Local)}
var onedaychild Person = Person{"Bob", "Roe", time.Date(2000, time.March, 5, 5, 10, 0, 0, time.Local)}

func TestPeopleLen(t *testing.T) {
	var expect int = 2
	t.Run("Equal", func(t *testing.T) {
		var ppl People = People{husband, wife}
		assert.Equal(t, expect, ppl.Len())
	})
	t.Run("NotEqual", func(t *testing.T) {
		var ppl People = People{husband, wife, twin01}
		assert.NotEqual(t, expect, ppl.Len())
	})
}

func TestPeopleLess(t *testing.T) {
	t.Run("ByBirthDay", func (t *testing.T) {
		var ppl People = People{husband, wife}
		assert.False(t, ppl.Less(0, 1))
	})
	t.Run("ByFirstName", func (t *testing.T) {
		var ppl People = People{twin01, twin02, onedaychild}
		assert.True(t, ppl.Less(0, 1))
	})
	t.Run("ByLastName", func (t *testing.T) {
		var ppl People = People{twin01, twin02, onedaychild}
		assert.True(t, ppl.Less(1, 2))
	})
}

func TestPeopleSwap(t *testing.T) {
	var ppl People = People{twin01, twin02, onedaychild}
	var expect People = People{twin02, twin01, onedaychild}
	ppl.Swap(0, 1)
	assert.Equal(t, expect, ppl)
}

///////////////////////////////////////////////////////////////////////////////////////////////////////

var strGood string = "1 2 3\n4 5 6\n7 8 9"
var strBadCols string = "1 2 3 5\n4 5 \n6 7 8 9 10"
var strBadContent string = "1 2 3\n4 a 6\n7 8 9"

func TestMatrixNew(t *testing.T) {
	t.Run("GoodMatrix", func (t *testing.T) {
		var expect Matrix = Matrix{3, 3, []int{1, 2, 3, 4, 5, 6, 7, 8, 9}}
		var r, err = New(strGood)
		if assert.NoError(t ,err) {
			assert.Equal(t, expect, *r)
		}
	})
	t.Run("BadLengthColums", func (t *testing.T) {
		var _, err = New(strBadCols)
		assert.Error(t ,err)
	})
	t.Run("BadContent", func (t *testing.T) {
		var _, err = New(strBadContent)
		assert.Error(t ,err)
	})
}

func TestMatrixRows(t *testing.T) {
	var expect [][]int = [][]int{{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}
	var m, err = New(strGood)
	if assert.NoError(t, err) {
		assert.Equal(t, expect, m.Rows())
	}
}

func TestMatrixCols(t *testing.T) {
	var expect [][]int = [][]int{{1, 4, 7}, {2, 5, 8}, {3, 6, 9}}
	var m, err = New(strGood)
	if assert.NoError(t, err) {
		assert.Equal(t, expect, m.Cols())
	}
}

func TestMatrixSet(t *testing.T) {
	var tests = []struct {
		r, c, v int
		want bool
	}{
		{1, 1, 10, true},
		{-1, 1, 10, false},
		{1, -1, 10, false},
		{5, 1, 10, false},
		{1, 10, 10, false},
	}
	var m, err = New(strGood)
	if assert.NoError(t, err) {
		for _, test := range tests {
			assert.Equal(t, m.Set(test.r, test.c, test.v), test.want)
		}
	} 
}
