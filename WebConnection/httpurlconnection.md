#HttpURLConnection

### GET
---
```
public boolean doGet(String targetURL) {
		boolean doSuccess = false;
		BufferedReader in = null;
		try {
			URL url = new URL(targetURL);
			HttpURLConnection URLConn = (HttpURLConnection) url
					.openConnection();
			URLConn.setRequestProperty(
					"User-agent",
					"Mozilla/5.0 (Windows; U; Windows NT 6.0; zh-TW; rv:1.9.1.2) "
							+ "Gecko/20090729 Firefox/3.5.2 GTB5 (.NET CLR 3.5.30729)");
			URLConn.setRequestProperty("Accept",
					"text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8");
			URLConn.setRequestProperty("Accept-Language",
					"zh-tw,en-us;q=0.7,en;q=0.3");
			URLConn.setRequestProperty("Accept-Charse",
					"Big5,utf-8;q=0.7,*;q=0.7");

			URLConn.setDoInput(true);
			URLConn.setDoOutput(true);
			URLConn.connect();
			URLConn.getOutputStream().flush();
			in = new BufferedReader(new InputStreamReader(
					URLConn.getInputStream(), "UTF-8"));

			String line;
			while ((line = in.readLine()) != null) {
				System.out.println(line);
			}

		} catch (IOException e) {
			doSuccess = false;
			e.printStackTrace();
		} finally {
			if (in != null) {
				try {
					in.close();
				} catch (java.io.IOException ex) {
					ex.printStackTrace();
				}
				in = null;

			}
		}

		return doSuccess;
	}
```
	
	
### POST
---
param[0] = URL</br>
param[i]... = other parameter....</br>
	
	
```
	public boolean doPost(String... param) {

		boolean doSuccess = false;
		java.io.BufferedWriter writer = null;
		try {

			URL url = new URL(param[0]);
			HttpURLConnection URLConn = (HttpURLConnection) url
					.openConnection();

			URLConn.setDoOutput(true);
			URLConn.setDoInput(true);
			((HttpURLConnection) URLConn).setRequestMethod("POST");
			URLConn.setUseCaches(false);
			URLConn.setAllowUserInteraction(true);
			HttpURLConnection.setFollowRedirects(true);
			URLConn.setInstanceFollowRedirects(true);

			URLConn.setRequestProperty(
					"User-agent",
					"Mozilla/5.0 (Windows; U; Windows NT 6.0; zh-TW; rv:1.9.1.2) "
							+ "Gecko/20090729 Firefox/3.5.2 GTB5 (.NET CLR 3.5.30729)");
			URLConn.setRequestProperty("Accept",
					"text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8");
			URLConn.setRequestProperty("Accept-Language",
					"zh-tw,en-us;q=0.7,en;q=0.3");
			URLConn.setRequestProperty("Accept-Charse",
					"Big5,utf-8;q=0.7,*;q=0.7");
			URLConn.setRequestProperty("Content-Type",
					"application/x-www-form-urlencoded");
			// URLConn.setRequestProperty("Content-Length", String.valueOf(data
			// .getBytes().length));

			java.io.DataOutputStream dos = new java.io.DataOutputStream(
					URLConn.getOutputStream());

			List<NameValuePair> params = new ArrayList<NameValuePair>();
			params.add(new BasicNameValuePair("lockId", param[1]));
			params.add(new BasicNameValuePair("time", param[2]));
			params.add(new BasicNameValuePair("operation", param[3]));

			writer = new BufferedWriter(new OutputStreamWriter(dos, "UTF-8"));

			writer.write(getQuery(params));
			writer.flush();
			writer.close();

			// Get Response
			InputStream is = URLConn.getInputStream();
			BufferedReader rd = new BufferedReader(new InputStreamReader(is));
			String line;
			StringBuffer response = new StringBuffer();
			while ((line = rd.readLine()) != null) {
				response.append(line);
				response.append('\r');
			}
			Log.d("Zack", response.toString());
			rd.close();
		} catch (java.io.IOException e) {
			doSuccess = false;
			e.toString();
		} finally {
			if (writer != null) {
				try {
					writer.close();
				} catch (java.io.IOException ex) {
					doSuccess = false;
					ex.toString();
				}
				writer = null;
			}
		}

		return doSuccess;
	}
```

###DELETE
---
```
public boolean doDelete(String targetURL, String userId) { 
	    boolean doSuccess = false; 
	    BufferedReader in = null;
	    java.io.BufferedWriter writer = null;
	    try { 
	      URL url = new URL(targetURL); 
	      HttpURLConnection URLConn = (HttpURLConnection) url 
	          .openConnection(); 
	 
	      URLConn.setDoOutput(true);
	      URLConn.setRequestProperty("Content-Type","application/json");   
	      URLConn.setRequestMethod("DELETE");
//	      URLConn.connect();
	      
	      java.io.DataOutputStream dos = new java.io.DataOutputStream(
					URLConn.getOutputStream());
			
			JSONObject jsonParam = new JSONObject();
			
			try {
				jsonParam.put("userId", userId);
			} catch (JSONException e) {
				e.printStackTrace();
			}

			writer = new BufferedWriter(new OutputStreamWriter(dos, "UTF-8"));

			writer.write(jsonParam.toString());
			writer.flush();
			writer.close();
	      
	      
//	      URLConn.setDoInput(true); 
//	      ((HttpURLConnection) URLConn).setRequestMethod("DELETE");
////	      URLConn.setDoOutput(true);
//	      URLConn.connect();
////	      URLConn.getOutputStream().flush();
	      in = new BufferedReader(new InputStreamReader(URLConn 
	          .getInputStream(), "UTF-8")); 
	 
	      String line; 
	      while ((line = in.readLine()) != null) { 
	        Log.d("Zack", line);
	      } 
	      doSuccess = true;
	    } catch (IOException e) { 
	      doSuccess = false; 
	      e.printStackTrace(); 
	    } finally { 
	      if (in != null) { 
	        try { 
	          in.close(); 
	        } catch (java.io.IOException ex) { 
	        	ex.printStackTrace();
	        } 
	        in = null; 
	      } 
	    } 
	 
	    return doSuccess; 
	  }
	  
```