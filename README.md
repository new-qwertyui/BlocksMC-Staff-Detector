# BlocksMC-Staff
List of all currently known BlocksMC staff. Contributions welcome!
 - List of known staff
 - Easy usability
## Example usage
```java


private boolean isStaffInGame() {
	assert mc.theWorld != null;
	for (EntityPlayer entity : mc.theWorld.playerEntities) {
		for (String name : getStaff()) {
			if (entity.getName().equalsIgnoreCase(name)) {
				return true;
			}
		}
	}
	return false;
}

private List<String> getStaff() {
	final List<String> staff = new ArrayList<>();
	try {
		HttpResponse res = httpsConnection("https://raw.githubusercontent.com/new-qwertyui/BlocksMC-Staff-Detector/refs/heads/main/List");
		if (res != null && res.getResponse() == HttpsURLConnection.HTTP_OK) {
			Scanner scanner = new Scanner(res.getContent());
			while (scanner.hasNextLine()) {
				staff.add(scanner.nextLine());
			}
			scanner.close();
		}
	} catch (Exception e) {
		e.printStackTrace();
	}
	return staff;
}

private static HttpResponse httpsConnection(String url) {
	try {
		HttpsURLConnection connection = (HttpsURLConnection) new URL(url).openConnection();
		connection.setRequestProperty("User-Agent", "WeedhackPremium");
		connection.connect();
		return new HttpResponse(readInputStream(connection.getInputStream()), connection.getResponseCode());
	} catch (IOException e) {
		e.printStackTrace();
	}
	return null;
}

public static String readInputStream(InputStream inputStream) {
	StringBuilder stringBuilder = new StringBuilder();
	
	try {
	    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(inputStream));
	    String line;
	    while ((line = bufferedReader.readLine()) != null)
		stringBuilder.append(line).append('\n');
	
	} catch (Exception e) {
	    e.printStackTrace();
	}
	return stringBuilder.toString();
}

@Getter // lombok
@AllArgsConstructor // lombok
private static class HttpResponse {
	private final String content;
	private final int response;
}
