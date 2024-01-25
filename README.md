# cheat-sheet
## GIT (Version Control)
##### Baru bikin
```
- echo "# sistem-upload" >> README.md
- git init
- git add README.md
- git commit -m "first commit"
- git remote add origin https://github.com/ngekoding/sistem-upload.git
- git push -u origin master
```
##### Mengatur Username & Email
```
- git config --global user.name "Nur Muhammad"
- git config --global user.email "blog.nurmuhammad@gmail.com"
* Cara diatas untuk mengatur disemua repositori, untuk spesifik hilangkan "--global"
```
##### PUSH
```
- git add .
- git commit -m "Your messages"
- git push -u origin master --> master is your "branch"
```
##### PULL
```
- git pull origin master
```
##### REMOVE
```
git rm file --> file is your file name
            --> and then, use PUSH
```
##### SHOW CONFIG
```
git config --list
```
##### REMOVE A COMMIT THAT ALREADY PUSHED
1. `git log` to find out the commit you want to revert
2. `git push origin +7f6d03:master` while `7f6d03` is the commit before the wrongly pushed commit. + was for force push

##### Merging without Auto-Merge
1. `git merge --no-commit --no-ff <local-branch>`
2. `git reset HEAD`
3. To see all diff: `git diff`

## PHP (How to do something?)
##### Remove HTML Tag from string
```
$content = strip_tags($content);
```
##### Get first image from string
```
preg_match('/<img.+src=[\'"](?P<src>.+?)[\'"].*>/i', $content, $image);
echo $image['src'];
```
##### Remove img tag from string
```
preg_replace("/<img[^>]+\>/i", "(image) ", $content);
echo $content;
```
##### Checking valid URL
```
public function valid_url($url) {
    if (!preg_match( '/^(http|https):\\/\\/[a-z0-9_]+([\\-\\.]{1}[a-z_0-9]+)*\\.[_a-z]{2,5}'.'((:[0-9]{1,5})?\\/.*)?$/i', $url)) {
        return FALSE;
    }
    return TRUE;
}
```

### PHPSpreadsheet

#### Without Template

```php
// For simple access
use PhpOffice\PhpSpreadsheet\IOFactory;
use PhpOffice\PhpSpreadsheet\Style\Border;
use PhpOffice\PhpSpreadsheet\Spreadsheet;
use PhpOffice\PhpSpreadsheet\Worksheet\Worksheet;
use PhpOffice\PhpSpreadsheet\Writer\Xlsx;
use PhpOffice\PhpSpreadsheet\Style\Alignment;
use PhpOffice\PhpSpreadsheet\Style\Fill;

$spreadsheet = new Spreadsheet();
$sheet = $spreadsheet->getActiveSheet();

// Write to cell
$sheet->setCellValue('A1', 'The Title');

// Merging
$sheet->mergeCells('A3:A4');

// Styling font (bold, sizing)
$sheet->getStyle('A1')
    ->getFont()
    ->setBold(TRUE)
    ->setSize(16);

// Setting column width
$sheet->getColumnDimension('A')->setWidth(5, 'px');

// Styling cell with array
$sheet->getStyle('A3:D4')
    ->applyFromArray([
        'font' => ['bold' => TRUE],
        'fill' => [
            'fillType' => Fill::FILL_SOLID,
            'color' => ['rgb' => 'EFEFEF'] 
        ],
        'alignment' => [
            'horizontal' => Alignment::HORIZONTAL_CENTER,
            'vertical' => Alignment::VERTICAL_CENTER,
        ]
    ]);

// Alignment
$sheet->getStyle('A'.$row)
    ->getAlignment()
    ->setHorizontal(Alignment::HORIZONTAL_CENTER);

// Bordering
$sheet->getStyle('A3:D4')
    ->getBorders()
    ->getAllBorders()
    ->setBorderStyle(Border::BORDER_THIN);

// Format currency
$sheet->getStyle('A3:A10')
    ->getNumberFormat()
    ->setFormatCode('#,##0.00');

// Format date
$date = \PhpOffice\PhpSpreadsheet\Shared\Date::PHPToExcel('2024-01-01'); // Requires to apply date format
$sheet->setCellValue('B1', $date);
$sheet->getStyle('B1')
    ->getNumberFormat()
    ->setFormatCode('dd/mm/yyyy');

$filename = 'Filename - '.time().'.xlsx';

header('Content-Type: application/vnd.openxmlformats-officedocument.spreadsheetml.sheet');
header('Content-Disposition: attachment;filename="'.$filename.'"');
header('Cache-Control: max-age=0');

$writer = new Xlsx($spreadsheet);
$writer->save('php://output');
```

#### Using Template

```php
$reader = IOFactory::createReader('Xlsx');
$spreadsheet = $reader->load('/path/totemplate.xlsx');
$spreadsheet->getProperties()
    ->setCreator('Document Creator')
    ->setTitle('Document Title');

$sheet = $spreadsheet->getActiveSheet();

// Add filename & header like before

$writer = IOFactory::createWriter($spreadsheet, 'Xlsx');
$writer->save('php://output');
```

## Helper

#### Checking date range availability

```php
function isDateRangeAvailable($conn, $dateStart, $dateEnd) {
    $sql = "SELECT * FROM bookings WHERE 
            (dateStart >= '$dateStart' AND dateEnd <= '$dateEnd') OR 
            (dateEnd >= '$dateStart' AND dateStart <= '$dateEnd')";

    $result = $conn->query($sql);

    if ($result->num_rows > 0) {
        // There are existing bookings that overlap with the specified date range
        return false;
    } else {
        // Date range is available
        return true;
    }
}
```

## CSS Tricks
#### CSS Triangle
```
.arrow-up {
  width: 0; 
  height: 0; 
  border-left: 5px solid transparent;
  border-right: 5px solid transparent;
  border-bottom: 5px solid black;
}

.arrow-down {
  width: 0; 
  height: 0; 
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
  border-top: 20px solid #f00;
}

.arrow-right {
  width: 0; 
  height: 0; 
  border-top: 60px solid transparent;
  border-bottom: 60px solid transparent;
  border-left: 60px solid green;
}

.arrow-left {
  width: 0; 
  height: 0; 
  border-top: 10px solid transparent;
  border-bottom: 10px solid transparent; 
  border-right:10px solid blue; 
}
```
