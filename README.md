// Define JSON schema
const schema = {
    "type": "object",
    "properties": {
        "name": {"type": "string"},
        "age": {"type": "number"}
    },
    "required": ["name", "age"]
};

// Sample JSON data
const jsonData = '{"name": "John Doe", "age": 30}';

// Function to validate JSON data against schema
function validateJson(jsonData, schema) {
    try {
        const data = JSON.parse(jsonData);
        // Validate JSON data against schema
        if (validate(data, schema)) {
            console.log("JSON data is valid.");
        } else {
            console.error("JSON data is not valid.");
        }
    } catch (error) {
        console.error("Invalid JSON data:", error.message);
    }
}

// Function to validate JSON object against schema
function validate(data, schema) {
    // Implement JSON validation logic here
    // Example: Check if all required fields are present
    for (const field of schema.required) {
        if (!(field in data)) {
            console.error(`Missing required field: ${field}`);
            return false;
        }
    }
    // Example: Check data types
    for (const [key, value] of Object.entries(data)) {
        const expectedType = schema.properties[key].type;
        if (typeof value !== expectedType) {
            console.error(`Invalid data type for ${key}. Expected ${expectedType}, got ${typeof value}`);
            return false;
        }
    }
    return true;
}

// Validate JSON data
validateJson(jsonData, schema);


....................................................



import xml.etree.ElementTree as ET

def is_json_like(xml_file):
    try:
        tree = ET.parse(xml_file)
        root = tree.getroot()

        # Check if the root has children (elements)
        if len(root) > 0:
            return False

        # Check if the root text can be loaded as JSON
        json.loads(root.text)
        return True

    except (ET.ParseError, ValueError):
        return False

# Example usage
xml_file = "example.xml"
if is_json_like(xml_file):
    print("The XML file appears to be in JSON format.")
else:
    print("The XML file is not in JSON format.")







    https://teams.microsoft.com/l/meetup-join/19%3ameeting_OWNmN2FjMjYtZTRiMi00MmY2LTlkZTItMDNhMTM4NzE1MGZj%40thread.v2/0?context=%7b%22Tid%22%3a%222e0cb644-c094-41d7-ab3d-43201da24438%22%2c%22Oid%22%3a%22d1503e4d-ccd0-484f-b7af-8ba8f391afbd%22%7d
