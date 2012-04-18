$document = 'sprawozdanie-interfejsy.pdf'
$dependencies = [
  'sprawozdanie-ato.sty',
  'tex/tytul.tex',
  'figury/ethernet/schemat-bez-konfiguracji.pdf',
  'figury/ethernet/schemat-po-konfiguracji.pdf',
  'tex/ethernet.tex',
  'tex/wifi.tex',
  'figury/bluetooth/schemat.png',
  'tex/bluetooth.tex',
  'tex/rs232.tex'
]
$byproducts = %w{*.out *.log *.aux *.toc}

$lc = 'xelatex'
$lf = '-interaction=nonstopmode'

file $document => [$document.sub('.pdf', '.tex'), *$dependencies] do |t|
  2.times { sh "#{$lc} #{$lf} #{t.prerequisites[0]} > /dev/null" }
end

task :default => :build

task :build => $document

task :show => $document do
  os = case `uname`.strip when 'Darwin' then :mac else :linux end
  case os
  when :mac
    sh "open #{$document}"
  else
    sh "xpdf #{$document} &"
  end
end

task :clean do
  $byproducts.each { |file| sh "rm -f #{file}" }
end
