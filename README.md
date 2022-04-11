<?php
class NQueen {
    public $queens;
    public $seat = array();
    public $result = array();

    function __construct($queens) {
        $this->queens = $queens; 
        $this->place(0); 
    }
 
    public function place($n) {
        if ($n == $this->queens) {
            $_result = array();
            for ($i = 0; $i < $this->queens; $i++) {
                $_result[] = $this->seat[$i];
            }
            $this->result[] = $_result;
            return;
        }
        for ($i = 0; $i < $this->queens; $i++) {
            $this->seat[$n] = $i;
            if ($this->checkPlace($n)) {
                $this->place($n + 1);
            }
        }
    }

    public function checkPlace($n) {
        for ($i = 0; $i < $n; $i++) {
            if ($this->seat[$i] == $this->seat[$n] || ($n - $i) == abs($this->seat[$i] - $this->seat[$n])) {
                return 0;
            }
        }
        return 1;
    }
}

$queen = new NQueen(8);
$result = $queen->result;

$j = 0;
foreach ($result as $v) {
    $j++;
    echo $j.'.<br>';
    echo '<table>';
    foreach ($v as $row) {
        echo '<tr align="center">';
        for ($i = 0; $i < count($v); $i++) {
            if ($row == $i) {
                echo '<td width="10">Q</td>';
            }
            else {
                echo '<td width="10">*</td>';
            }
        }
        echo "</tr>";
    }
    echo "</table><br>";
}
?>
