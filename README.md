# SPO Recursive File Upload

Upload a file, or files, to SharePoint Online using the `spsave` package.

## Inputs

`site_url`: Destination SPO site URL  
`username`: SPO account username. **Must have write privileges on the designated site.**  
`password`: SPO account password.  
`destination_path`: Relative destination path on SPO site. If path does not exist, it will be created.  
`source_path`: Source file path(s) to be uploaded to SPO. Separate multiple files using a semicolon `;`.
`base`: If you want to preserve folders structure inside SharePoint folder, you can provide a base for you files. For example when using glob ['build/css/*.*'] and base: 'build', all css files will be loaded under [SharePoint folder]/css.  

## Things you need to know

- Files are directly uploaded via the `glob` method in the `spsave` package.
- SPO account must not have multi-factor authentication turned on, or must use an application-specific password. Service accounts are preferred.
- Multiple files are uploaded to the same destination path.
- run `npm install` to get packages
- Pack is complied using vercel/ncc
  - install using `npm i -g @vercel/ncc`
  - compile dist using: `ncc build index.js --license licenses.txt`
  - action.yml points to dist/index.js for this reason, the index.js in the root is purely for development. 
  - Make sure to run `ncc build index.js --license licenses.txt` before committing any changes to github

## Example Usage

```yaml
...
uses: ukho/spo-recursive-file-upload@vversion
with:
  site_url: https://domain.sharepoint.com/sites/my-site
  username: ${{ secrets.SPO_USERNAME }}
  password: ${{ secrets.SPO_PASSWORD }}
  destination_path: Shared Documents
  source_path: dist/my-file.txt
  base: dist
  # or for multiple files
  # source_path: dist/my-file1.txt;dist/my-file2.txt
...
```

## Issues

This is released under an MIT any issues please feel free to take a copy, we will not be handling issues outside of our own use cases.

## Credits

This base application was taken from [s-KaiNet's SPSave](https://github.com/s-KaiNet/spsave).
