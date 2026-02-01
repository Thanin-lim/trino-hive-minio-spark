config notebook jupyter ให้ version python ตรงกันกับ spark 



docker exec -it  ชื่อ jupyter แล้วก็ bash
# สร้าง environment ชื่อ py38
conda create -n py38 python=3.8 ipykernel -y
# สลับมาใช้ py38
conda activate py38
# สร้าง Kernel ชื่อ "Python 3.8 (Spark)"
python -m ipykernel install --user --name=py38 --display-name "Python 3.8 (Spark)"

# token ดูได้ใน log jupyter"






