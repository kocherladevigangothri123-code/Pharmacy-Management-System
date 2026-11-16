package com.pharmacy.controller;

import com.pharmacy.model.Medicine;
import com.pharmacy.model.Sale;
import com.pharmacy.repository.MedicineRepository;
import com.pharmacy.repository.SaleRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.time.LocalDateTime;
import java.util.List;

@RestController
@RequestMapping("/api/pharmacy")
public class PharmacyController {

    @Autowired
    private MedicineRepository medicineRepository;

    @Autowired
    private SaleRepository saleRepository;

    // 1. Get all medicines
    @GetMapping("/medicines")
    public List<Medicine> getAllMedicines() {
        return medicineRepository.findAll();
    }

    // 2. Add a new medicine
    @PostMapping("/medicines")
    public Medicine addMedicine(@RequestBody Medicine medicine) {
        return medicineRepository.save(medicine);
    }

    // 3. Delete a medicine
    @DeleteMapping("/medicines/{id}")
    public String deleteMedicine(@PathVariable Long id) {
        medicineRepository.deleteById(id);
        return "Medicine deleted successfully with ID: " + id;
    }

    // 4. Low stock alerts
    @GetMapping("/medicines/low-stock")
    public List<Medicine> getLowStock() {
        return medicineRepository.findByStockLessThanEqual(15);
    }

    // 5. Get all sales history
    @GetMapping("/sales")
    public List<Sale> getAllSales() {
        return saleRepository.findAll();
    }
}
