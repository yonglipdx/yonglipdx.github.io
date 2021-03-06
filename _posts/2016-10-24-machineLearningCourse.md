## Machine Learning 

### Lecture one: Introduction

* **supervised learning**
  * We are given a data set and alredy know what our correct output should look like, having the idea that there is a relationship between the input and the output.
    * **regression**
      * predict results within a continuous output
      * map input variables into discrete categories 

* **unsupervised learning**
  * approach problem with little or no idea what our results shold look like.
    * with unsupervised learning, there is no feedback based on the prediction results.
    * we can derive the structure by clustering the data on relationship amount the variables in the data.
   



1. [**STL containers**](http://www.cs.northwestern.edu/~riesbeck/programming/c++/stl-summary.html)
2. [**c++11 basic**](http://blog.kavinyao.com/2014/02/cpp11-features)
3. [**c++11 basic_2**](http://www.codeproject.com/Articles/570638/Ten-Cplusplus11-Features-Every-Cplusplus-Developer)


* string
   * s.size(), s.find(str2) $std::size_t/$std::npos, s.replace(start,len,str2), [], str.swap(str2), str.pop_back(), str.append(s2), s.push_back('c'), s.insert(pos, str2), s.compare(s2) $0/-1/1

* auto loop

          using namespace std;
          auto p = m.begin();
          auto p = new T();
          for( auto d : m);
          for( auto& d : m);
          vector<int> m;

* unordered_map

          std::unordered_map<std::string,double> mymap = {
             {"mom",5.4},
             {"dad",6.1},
             {"bro",5.9}
          }; 
          mymap.insert({ {"brother",0.8}, {"sister",0.9} });
          mymap["uncle"] = 3.3;

          mymap.erase("dad"); 
          mymap.erase(mymap.find("uncle");

          auto got = mymap.find ("mom");
          if ( got != mymap.end() )
          std::cout << got->first << " is " << got->second;

          for (auto& i : mymap){
             cout << i->first << ": " << i->second << endl;
          }

          mymap.size();
          mymap.clear();

* stack (push, pop, empty, size, swap, top)    -> pop on top
* queqe (push, pop, empty, size, swap, front, back) -> pop on front

          using namespace std;
          std::queue<int> myqueue;
          int myint;
          myqueue.push(1);
          while (!myqueue.empty())
          {
             std::cout << ' ' << myqueue.front();
             myqueue.pop();
          }
          myqueue.swap(myqueqe2);

* vector(push_back(), pop_back(); size(), empty(), 
   - Insert $$urn to the first of added element

          std::vector<int> myvector (3,100);
          auto it = myvector.begin();
          it = myvector.insert ( it , 200 );
          myvector.insert (it,2,300);

          // "it" no longer valid, get a new one:
          it = myvector.begin();

          std::vector<int> anothervector (2,400);
          myvector.insert (it+2,anothervector.begin(),anothervector.end());

          int myarray [] = { 501,502,503 };
          myvector.insert (myvector.begin(), myarray, myarray+3);

          std::cout << "myvector contains:";
          for (it=myvector.begin(); it<myvector.end(); it++){
             std::cout << ' ' << *it;
          }
          //myvector contains: 501 502 503 300 300 400 400 200 100 100 100

    - erase $ an iterator pointing to the new location of the element that followed the last element erased by the function call

          std::vector<int> myvector;
          for (int i=1; i<=10; i++) myvector.push_back(i);

          // erase the 6th element
          auto p = myvector.erase (myvector.begin()+5);
          // p point to 7 

          // erase the first 3 elements:  [first, last)
          auto p = myvector.erase (myvector.begin(),myvector.begin()+3);


* unique_ptr
   - basic

          class Foo
          {
          public:
             Foo() { std::cout << "+++ Foo::Foo()\n"; }
             ~Foo() { std::cout << "--- Foo::~Foo()\n"; }
             void process() { std::cout << "... Foo::process()\n"; }
          };

          int main(int argc, char* argv[])
          {
             std::cout << "+++ main()\n";

             std::unique_ptr<Foo> obj(new Foo);
             obj->process();

             std::cout << "--- main()\n";

             return 0;
          }
          /* output
          +++ main()
          +++ Foo::Foo()
          ... Foo::process()
          --- main()
          --- Foo::~Foo()
          */

          std::unique_ptr<Foo> obj1(new Foo);   j
          std::unique_ptr<Foo> obj2;
          obj2 = obj1;             // Wrong
          obj2 = std::move(obj1);  // Right

   - Array of unique_ptr

          const unsigned N = 10;
          std::unique_ptr<Foo[]> objarray(new Foo [N]);
          for (unsigned i = 0; i < N; i++)
          {
             std::cout << i << " ";
             objarray[i].process();
          }

   - Returing obj from function

          // This object will be freed when the caller stops refereeing it
          std::unique_ptr<Foo> make_foo()
          {
             std::unique_ptr<Foo> obj(new Foo);

             // prepare obj

             return obj;
          }

   - Container of unique_ptr
          std::vector< std::unique_ptr<Foo> > v;
          std::unique_ptr<Foo> q(new Foo(i));
          v.push_back(std::move(q));

* sort    

 ![sort_comparison]({{ site.url }}/images/sort_comparison.PNG)

   
1. class member initialize  
        typedef struct testStruct{
         int a;
        } struct_a, *struct_a_p;

        class A
        {
        public:
         A() {}
         A(int in_a) : a(in_a) {}
         A(C c) {}
        private:
         int a = 4;
         int b = 2;
         string h = "text1";
         string s = "text2";
        }

2. prefer auto in the following case
        //Here is T in the expression. No need to repeat it again.
        auto p = new T();
        auto p = make_shared<T>(arg1);

        //If you need to store lambda you may use auto or std::function
        auto my_lambda = [](){};

        //Instead of: map<string,list<int>::iterator>::const_iterator it = m.cbegin(); 
        auto it = m.begin();

3. Range for/begin/end
        vector<int> v;
        for( auto d : v )
           total += d;
        int a[] = {1,2,3,4,5};
        sort( begin(a), end(a) );


# Lex
	Scanner produces a stream of tokens from the input source.
	lex is a scanner generator.
	lex input is set of regular expressions and associated action (wirtten in C)
	lex output is a table-driven scanner (lex.yy.c)
	flex: an open source implementation of lex.

	# lex input
		first part (optional)
		table size demision
		defination of text replacement
		global C code (specail syntax required)
		...
		%% -----> termination of FIRST PART
		pattern	action
		regular expression and action
		action and be C statment or block of C code.
		...
	 	%% ------> termination of SECOND PARt
		Third PART (optional)
		C code simplied used as is.

	Example: filename: exl.l
	--------
	%%
	"hello world"	printf("goodbye\n");
	.		;  ----> ignore everthing other than "hello world"
	%%
	--------

	lex exl.1 ----> generate a scanner, saved as lex.yy.c
	cc lex.yy.c -ll  (with -ll option main() is grab from the lex library)


	Example2: suppose we have configuration file "config.in"
	--------

# yacc

# MISCELLANEOUS
  ## char* const vs    const char*
            according to the standard, const modifies the element directly to its left. 
            The use of const at the beginning of a declaration is just a convenient mental shortcut. 
            So the following two statements are equivalent:
            char const * pointerToConstantContent1;
            const char * pointerToConstantContent2;

            In order to ensure the pointer itself is not modified, 
            const should be placed after the asterisk:
            char * const constantPointerToMutableContent;

            To protect both the pointer and the content to which it points, use two consts.
            char const * const constantPointerToConstantContent;

## stringstream:
	example1: 
	  string a("123");
          stringstream ss(a);
	  ss << "456"
	  cout << aa.str(); ---> 456

        example2:
	  string a("123");
          stringstream ss("");
	  ss << a << << "456"
	  cout << aa.str(); ---> 123456

## ssize_t size_t
        to avoid i == -1

        size_t i: 
                 if (i > -1) // not OK since i always > -1
                 use i< (size_t)-1  to make sure i > -1;

        ssize_t i: 
		 i > -1 is OK since i could be -1 in ssize_t




