package coverage

import (
	"fmt"
	"os"
	"reflect"
	"testing"
	"time"
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

var husband Person = Person{"John", "Doe", time.Date(1970, time.January, 1, 1, 1, 0, 0, time.Local)}
var wife Person = Person{"Jane", "Doe", time.Date(1973, time.March, 3, 3, 3, 0, 0, time.Local)}
var twin01 Person = Person{"Ann", "Doe", time.Date(2000, time.March, 5, 5, 10, 0, 0, time.Local)}
var twin02 Person = Person{"Bob", "Doe", time.Date(2000, time.March, 5, 5, 10, 0, 0, time.Local)}
var onedaychild Person = Person{"Bob", "Roe", time.Date(2000, time.March, 5, 5, 10, 0, 0, time.Local)}

func TestPeople_Len(t *testing.T) {
	var ppl People = People{husband, wife}
	var expect int = 2
	r := ppl.Len()
	if r != expect {
		t.Errorf("Expected: %d, got %d", expect, r)
	}
}

func TestPeople_LessByBirthDay(t *testing.T) {
	var ppl People = People{husband, wife}
	var a, b int = 0, 1
	var expect bool = true
	r := ppl.Less(a, b)
	if r {
		t.Errorf("Expected: %t, got %t", expect, r)
	}
}

func TestPeople_LessByFirstName(t *testing.T) {
	var ppl People = People{twin01, twin02, onedaychild}
	var a, b int = 0, 1
	var expect bool = false
	r := ppl.Less(a, b)
	if !r {
		t.Errorf("Expected: %t, got %t", expect, r)
	}
}

func TestPeople_LessByLastName(t *testing.T) {
	var ppl People = People{twin01, twin02, onedaychild}
	var a, b int = 1, 2
	var expect bool = false
	r := ppl.Less(a, b)
	if !r {
		t.Errorf("Expected: %t, got %t", expect, r)
	}
}

func TestPeople_Swap(t *testing.T) {
	var ppl People = People{twin01, twin02}
	var expect People = People{twin02, twin01}
	var i, j int = 0, 1
	ppl.Swap(i, j)
	for k, v := range ppl {
		if v != expect[k] {
			t.Errorf("Expected: %v, got %v", expect, ppl)
		}
	}

}

///////////////////////////////////////////////////////////////////////////////////////////////////////

func TestMatrix_NewGoodMatrix(t *testing.T) {
	var str string = "1 2 3\n4 5 6\n7 8 9"
	var expect Matrix = Matrix{3, 3, []int{1, 2, 3, 4, 5, 6, 7, 8, 9}}
	var r, err = New(str)
	if err != nil {
		t.Errorf("Expected to get nil, but actual is %v", err)
	}
	if !reflect.DeepEqual(*r, expect) {
		t.Errorf("Expected: %v, got %v", expect, *r)
	}
}

func TestMatrix_NewBadColunsLength(t *testing.T) {
	var str string = "1 2 3 5\n4 5 \n6 7 8 9 10"
	var _, err = New(str)
	if err == nil {
		t.Errorf("Expected error: %v, but get nil", err)
	}
}

func TestMatrix_NewBadContent(t *testing.T) {
	var str string = "1 2 3\n4 a 6\n7 8 9"
	var _, err = New(str)
	if err == nil {
		t.Errorf("Expected error: %v, but get nil", err)
	}
}

func TestMatrix_Rows(t *testing.T) {
	var str string = "1 2 3\n4 5 6\n7 8 9"
	var expect [][]int = [][]int{{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}
	var m, err = New(str)
	if err != nil {
		t.Errorf("Unexpected error: %v", err)
	}
	if !reflect.DeepEqual(m.Rows(), expect) {
		t.Errorf("Expected: %v, but got %v", expect, m.Rows())
	}
}

func TestMatrix_Cols(t *testing.T) {
	var str string = "1 2 3\n4 5 6\n7 8 9"
	var expect [][]int = [][]int{{1, 4, 7}, {2, 5, 8}, {3, 6, 9}}
	var m, err = New(str)
	if err != nil {
		t.Errorf("Unexpected error: %v", err)
	}
	if !reflect.DeepEqual(m.Cols(), expect) {
		t.Errorf("Expected: %v, but got %v", expect, m.Rows())
	}
}

func TestMatrix_Set(t *testing.T) {
	var str string = "1 2 3\n4 5 6\n7 8 9"
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
	var responce bool
	var m, err = New(str)
	if err != nil {
		t.Errorf("Unexpected error: %v", err)
	}
	for _, test := range tests {
		tName := fmt.Sprintf("r:%d,c:%d,v:%d,w:%t",test.r,test.c,test.v,test.want)
		t.Run(tName, func (t *testing.T) {
			responce = m.Set(test.r, test.c, test.v)
			if  responce != test.want {
				t.Errorf("Expected: %v, but got %v", test.want, responce)
			}
		})
	}
}