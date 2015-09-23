#Threading

##AsyncTask


#####main class
type1 for doInBackground
type2 for onProgressUpdate
type3 for onPostExecute

```
class MyAsyncTask extends AsyncTask<String, Integer, Boolean>{
		private final static String URL = "http://192.168.0.170:8080/smartlock_cloud/services/command/operation/";
		@Override
		protected void onPreExecute() {
			super.onPreExecute();
		}

		@Override
		protected String doInBackground(String... param) {
			
		}
		
		@Override
		protected void onProgressUpdate(Integer... progress){
         setProgressPercent(progress[0]);
        }

		@Override
		protected void onPostExecute(Boolean result) {
			super.onPostExecute(result);
		}

	}
```
#####calling
```
new MyAsyncTask().excute(String p1, String p2,.........);
```