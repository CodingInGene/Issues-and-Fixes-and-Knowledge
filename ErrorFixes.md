**	Django-

IntegrityError-
    Check if your table has data in it and if you are trying to input
    same ID or any unique constraints multiple times.
    Clear all data or any specific then try.

NoReverse at / -
    use of 'Redirect'- redirect('')
    like this-
    if request.method == "GET":
        #Student.objects.create(**d)
        return HttpResponseRedirect('')     #returns this first
        
    return render(request,'crudhome.html')  #Cannot render the page

    Try this method-
        1.Make temp website. make at urls.py (let's say- 'redirect')

        2.After clicking submit btn in html redirect to that site (If home 
         url is 'localhost:8000/home' then redirect to 'redirect', in 'urls.py'
         it will be 'redirect/'.)

        3.The views.py will be->
            def home(request):
                #Redirecting to a temp site to store data and then 
                #again redirecting to home via html button
                return render(request,'crudhome.html')

            def redirected(request):
                d={
                    "name":request.GET.get('name'),
                    "title":request.GET.get('title'),
                    "desc":request.GET.get('desc')
                }
                print(d)
                if request.method == "GET" and request.GET.get('name') != "":
                    Student.objects.create(**d)
                    print(d)
                
                return redirect('homepage') #redirect uses name of the page in 'urls'

        So the method is-
            Home - form submission - redirect to temp site -
            -> store data - redirect to main page






**	Node JS-

1.
Setup backend for azure sql-
error- ODBC file not found.
install odbc dependencies in node project-

-> sudo add-apt-repository "$(curl -fsSL https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/prod.list)"

-> sudo apt-get install -y unixodbc unixodbc-dev odbcinst odbcinst1debian2 libodbc1

-> sudo apt-get install -y msodbcsql17

if still not running, after these- npm i odbc (On the project to declare it as dependency)


2.
Argument of type 'Promise<any>' is not assignable to parameter of type 'SetStateAction<never[]>' error in next js fetch api
code-
useEffect(()=>{
    async function getData(){
      const response = fetch('localhost:8080/api');
      const d = (await response).json();
      setData(d);
    }
  });
  
Ans-
useEffect(()=>{
    async function getData(){
      const response = fetch('localhost:8080/api');
      
      const d = await Promise.resolve((await response).json());		**
      
      setData(d);
    }
  });
  
  
 3.
 Objects Are Not Valid as a React Child - error in next js-
 
 response from server - {name:"avoy", age:"23"}
 
 in next js -
 export default function Home() {
  const [data,setData] = useState();
  useEffect(() => {
    async function getData(){
      const response = fetch("http://localhost:8080/api");
      const jsonData = await Promise.resolve((await response).json());
      setData(jsonData);
      console.log(jsonData);
    }

    getData();
  },[]);
  return (
    <div>
      <h1>{JSON.stringify(data)}</h1>	** This will not work because to print in h1 string is needed not JSON- use stringify
    </div>
  );
}

Solution-
 <h1>{JSON.stringify(data)}</h1>
 
 

**	Snapd removed by mistake but not completely removed-
sudo systemctl stop var-snap-firefox-common-host\\x2dhunspell.mount
sudo systemctl disable var-snap-firefox-common-host\\x2dhunspell.mount
sudo apt remove --purge snapd
sudo apt install snapd




