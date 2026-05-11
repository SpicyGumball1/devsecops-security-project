# GSLC-2-DEVSECSOPS
# =========================================
# ANALISIS RELIABILITY SISTEM TOKONET
# =========================================

# Dataset downtime
incidents = [
    {
        "incident_id": 3,
        "durasi": 7,
        "status": "down",
        "cause": "possible DDoS"
    },
    {
        "incident_id": 5,
        "durasi": 6,
        "status": "down",
        "cause": "possible DDoS"
    },
    {
        "incident_id": 7,
        "durasi": 8,
        "status": "down",
        "cause": "possible DDoS"
    },
    {
        "incident_id": 9,
        "durasi": 8,
        "status": "down",
        "cause": "possible DDoS"
    },
    {
        "incident_id": 12,
        "durasi": 15,
        "status": "down",
        "cause": "maintenance"
    }
]
# =========================================
# TOTAL WAKTU PENGAMATAN
# =========================================

hari_pengamatan = 3
menit_per_hari = 24 * 60

total_waktu = hari_pengamatan * menit_per_hari

# =========================================
# TOTAL DOWNTIME
# =========================================

total_down = sum(incident["durasi"] for incident in incidents)

# =========================================
# TOTAL UPTIME
# =========================================

total_up = total_waktu - total_down

# =========================================
# JUMLAH FAILURE
# =========================================

jumlah_failure = len(incidents)

# =========================================
# PERHITUNGAN MTTR
# =========================================

MTTR = total_down / jumlah_failure

# =========================================
# PERHITUNGAN MTTF
# =========================================
MTTF = total_up / jumlah_failure

# =========================================
# PERHITUNGAN MTBF
# =========================================

MTBF = MTTF + MTTR

# =========================================
# PERHITUNGAN AVAILABILITY
# =========================================

availability = (MTTF / (MTTF + MTTR)) * 100

# =========================================
# AVAILABILITY HARI KEDUA
# =========================================

# downtime hari kedua
hari_kedua_down = 7 + 6 + 8 + 8

# uptime hari kedua
hari_kedua_up = 1440 - hari_kedua_down

# availability hari kedua
availability_hari_kedua = (hari_kedua_up / 1440) * 100

# =========================================
# PERHITUNGAN KERUGIAN BISNIS
# =========================================

pendapatan_per_menit = 500000
kerugian = total_down * pendapatan_per_menit

# =========================================
# OUTPUT PROGRAM
# =========================================
print("=== ANALISIS RELIABILITY TOKONET ===")
print()

print(f"Total waktu pengamatan : {total_waktu} menit")
print(f"Total downtime         : {total_down} menit")
print(f"Total uptime           : {total_up} menit")
print(f"Jumlah failure         : {jumlah_failure}")
print()

print(f"MTTR                   : {MTTR:.2f} menit")
print(f"MTTF                   : {MTTF:.2f} menit")
print(f"MTBF                   : {MTBF:.2f} menit")
print(f"Availability           : {availability:.2f}%")
print()

print("=== AVAILABILITY HARI KEDUA ===")
print(f"Availability Hari 2    : {availability_hari_kedua:.2f}%")
print()

print("=== ESTIMASI KERUGIAN ===")
print(f"Total kerugian         : Rp {kerugian:,}")
