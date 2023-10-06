# fileupload

 string apiUrl = "https://localhost:7039"; // Replace with your API URL
                string downloadEndpoint = $"{apiUrl}/Admin/Category/DownloadFiless?version={version}";
        [AllowAnonymous]
        public IActionResult DownloadFiless(string version)
        {
            try
            {
                // Find the file based on the version
                var file = _unitOfWork.FILES.GetFileByVersionAsync(version).Result; // Assuming GetFileByVersionAsync is synchronous

                if (file != null)
                {
                    var filePath = file.FilePath;

                    // Get the file content
                    var fileBytes = System.IO.File.ReadAllBytes(filePath);
                    var fileName = file.FileName;

                    // Return the file as a byte array
                    return File(fileBytes, "application/octet-stream", fileName);
                }
                else
                {
                    // File not found for the given version
                    ToastrError("File not found for the specified version.");
                    return RedirectToAction("Upload");
                }
            }
            catch (Exception ex)
            {
                ToastrError("Error downloading file: " + ex.Message);
                return RedirectToAction("Upload");
            }
        }
